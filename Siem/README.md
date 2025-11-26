# SIEM and IDPS
### Tools used to accomplish todays Labs:
- Suricata (open-source IDPS)
- Loki (Log Database) (bassically light weight Elaticsearch)
- PromTail (Log Shipper)(tails log files and directs them to loki)
- LogCLI (Means of quereying Loki) 
- Docker (we all know and love it)(containerization for those who don't know)

### Getting Started
`sudo apt update; sudo apt upgrade`
`curl -fsSL https://get.docker.com | sudo sh` this gets the latest version
`sudo apt install jq curl unzip` 

Now we're going to create a docker group to prevent writing sudo a hundred million times.

`groupadd -U $USER docker` create new group 'docker' and add self to it

Then log out and login or run `newgrp docker` to apply changes

Run `docker -V` to verify everything is working

Lets get suricata working now; install and update
```
sudo apt -y install suricata;
sudo apt -y install suricata-update;
sudo suricata-update;
```
This should output a bunch of install logs from the system and a bunch of logs from suricata about updating rules.

Now we have to update the suricata yaml config. First lets get our interface name 

`ip -br a | awk '$1!="lo"{print $1, $3}'`

a quick breakdown of this is 
- `ip` is the linux networking tool
- `a` | `addr` the argument to get addresses
- `-br` is the flag for a brief output

The second command `awk` that we're piping into is a formatting/filtering tool 
-  `'$1!="lo"{print $1, $3}'` this means that for each line whom's column 1 doesn't equal lo (loopback interface) we print column 1 and column 3

mine outputs 
```
enp9s0 192.168.1.95/24
wlp7s0 
docker0 172.17.0.1/16
```

now lets make the directory to set custom rules
```
sudo mkdir -p /etc/suricata/rules
sudo touch /etc/suricata/rules/local.rules
```
- `-p` in mkdir is for parent meaning to  for make all the subdirectories in the path specified

Then use a text editor to add your rule file to the suricata yaml file. I like vi because of how easy it is to locate the lines I'm looking for.

To verify the suricata connection run:
`sudo suricata -T -c /etc/suricata/suricata.yaml -v`

- `-T` is the flag to test the configuration
- `-c` is the flag to specify the path to the config file
- `-v` increases the verbosity od the application, this flag is specifically for the INFO

Now lets run suricata:

This command stops the current service
`sudo systemctl stop surcata`

This command start the service again in the backgroud while using the first interface name from a prior command (enp9s0)

`sudo surcata -i $(ip -br a | awk '$1!="lo" {print $1; exit}') -D` 
- `-i` is to specify additional config files
- `-D` is to bind the program's processes to the current shell's instance

The first command shouldn't have an output then the second command should tlle you that suricata is running in system mode.

To confirm that the program is properly logging we can run:

`sudo tail -f /var/log/suricata/eve.json | jq .` 

The following command allows us to peek at the eve.json file that records all IDPS events jq makes it easier to read.

`sudo jq . /var/log/suricata/eve.json`

This file has json objects with attributes such as 'event_type' which tells you whether or not the event logged is an anomoly or quic which is a special protocol in suricata which does a number of things. 

---

## Loki 

This program is the means of aggregating logs across your system. It was developed by Grafana Labs. Their approach to creating the app was brilliant, instead of a all for one tool, they made a bunch of smaller tools and aggregated those to work in unison. This allows for greater control from the user over their project. 

The app consists of three components: the first being promtail which simply sends all logs to Loki, promtail can have multiple instances for different logging applications. Then loki is the component that stores the logs by indexing labels of each log entry. This is efficient for searching and filtering later on. The final component is called Grafana, which is the means to visualize the logs in contexts like charts/graphs.

To deploy its recomended to use Docker to allow for a sequential configuration. 
Some log filers for loki include: 
- Event
- Server
- System
- Authorization
- Change
- Availability
- Resource
- Threat

To start setting Loki up we have to first create the conf directories and config files. 

`sudo mkdir -p /etc/loki /var/lib/loki/{chunks,rules}` 
- `{chunks, rules}` makes equal level subdirectories at the path specified. So we'll have .../loki/chunks and .../loki/rules

Now lets make a default [loki_conf](./loki-config.yaml). 

Here are some highlighted features from this config:
- `auth_enabled: false` turns off auth for simplicity
- `server.http_listen_port_3100` look at specified port for incoming connections
- `conjnom.path_prefix` and ` storage.filesystem` defined where logs should be stored
- `schema_config` tells loki how to structure and index logs.

Now lets fix the file permissions to the program so it can write to the directories we made.

```
sudo chown -R 10001:10001 /var/lib/loki
sudo chmod -R u+rwX /var/lib/loki
```

Now all that is left to do is start Loki

```
sudo docker run -d --name loki -p 3100:3100 \
 -v /etc/loki:/etc/loki \
 -v /var/lib/loki:/var/lib/loki \
 grafana/loki:2.9.8 -config.file=/etc/loki/loki-config.yml
 ```
 - `-name` is to provide a container name
 - `-d` is for running the container in the background
 - `-p` is to map ports from container to the host's 
 - `-v` is for volume mapping specified directory in the container to the other specified directory on the host  
 - `grafana/...` is to specify the base image from dockers internal repo of images.

to verify everything is working run docker ps to see if the container is running. My didn't at first due to a malformed config file. I used `docker log loki` to id the issue

The port loki our program exposes is 3100. It is in the docker command after the -p and in the curl command. It uses the api route `/loki/api/v1/push` to accept log data.

---
## Promtail

First make the associated directories:

`sudo mkdir -p /etc/promtail /var/lib/promtail`

Then copy the promtail file to its correct path <u>/etc/promtail</u> 

I just copied it from my repo into the dir just specified

Then just run promtail in another container.

```
sudo docker run -d --name promtail -p 9080:9080 \
 -v /etc/promtail:/etc/promtail \
 -v /var/log/suricata:/var/log/suricata:ro \
 -v /var/lib/promtail:/var/lib/promtail \
 grafana/promtail:2.9.8 \
 -config.file=/etc/promtail/promtail-config.yml
```

notice how we do the pattern of volume mapping as with loki, but we use a different base image to, one made for promtail.

Promtail is simply just the messenger between the IDPS and Loki the log aggregator. The position file is simply the offset for each log file its monitoring. This prevents promtail from passing duplicate data to loki and lack of data getting to loki. 

I had to download the binaries for an amd64 because I'm running an x86_64 machine. 

Here is the install commands if you have a machine like mine:

`curl -Lo /tmp/logcli.zip https://github.com/grafana/loki/releases/download/v2.9.8/logcli-linux-amd64.zip`

This installs the binaries for the program to <u>/tmp/logcli.zip</u> 

The following command extracts the decompressed binaries from the compressed version we have. We extract them to the directory <u>/usr/local/bin</u> 

`sudo unzip -o /tmp/logcli.zip -d /usr/local/bin`

Now we have to grap the unzipped binaries for the program and rename the folder to <u>/logcli</u>. We do this because when we execute logcli we want the system to look for the directory 'logcli' in /usr/bin whereas it's currently named <u>/logcli-linux-amd64</u>

`sudo mv /usr/local/bin/logcli-linux-amd64 /usr/local/bin/logcli`

Now make it executeable with:

`sudo chmod +x /usr/local/bin/logcli`

Verify everything worked with 

`logcli --version`

Now we should list avaialable labels wiht the `label` argument: 

`logcli labels --addr=http://localhost:3100`
- `--addr=` is the flag to specify a target ip with protocol

I got the output 
```
2025/11/22 15:49:05 http://localhost:3100/loki/api/v1/labels?end=1763844545562601364&start=1763840945562601364
```
Since no labels are printed out we know loki has not recieved any log streams with labels

Now lets get recent query logs with the `query` argument:

`logcli query --addr=http://localhost:3100 --limit=10 '{job="suricata"}'`
- `--limit=` is the flag to specify a limit to the amount of queries returned.
- the `'{}'` is to filter output by parameter we filer by jobs relating to suricata

I got the output: 
```
2025/11/22 15:49:46 
http://localhost:3100/
loki/api/v1/query_range?
direction=BACKWARD&end=1763844586832275629&
limit=10&
uery=%7Bjob%3D%22suricata%22%7D&
start=1763840986832275629
``` 

Labels and full-text indexes differ in the sense that logs only provide metadata of the log whereas full-text provide every word in the log.

---

## Generating alerts:

```
echo 'alert http any any -> any any (msg:"LAB UA hit"; http.user_agent; content:"CPS-NETSEC-LAB"; sid:9900001; rev:1;)' \
| sudo tee -a /etc/suricata/rules/local.rules
```
- We're using `echo` to pipe text to `tee` which simply takes text in and writes to another place. 
- `alert` generate an alert when ...
- `http any any -> any any` means any HTTP request directed or coming from any ip 
- `msg:"LAB UA hit";` means generate message saying "LAB UA hit"
- `http.user_agent content:"CPS-NETSEC-LAB";` means only when user-agent string is "CPS-NETSECLAB"
- `sid:9900001;` assigns a signature ID to identify the alert
- `rev:1` is the version of your rule. (update as necessary)

To apply the rule we must do:
`sudo systemctl restart suricata`

Now lets trigger the alert to verify our rule works:

`curl -A "CPS-NETSEC-LAB" http://example.com/ || true`

After getting this far I realized my promtail config wansn't properly tabbed so I went back and fixed that.

Then I had issues because my suricata was listening to the wrong interface. Since I am not in a vm I had to manually to _enp9s0_ 

I regenerated the alert with the command above. Then ran the following to verify:

`logcli query --addr=http://localhost:3100 --limit=50 '{job="suricata"} |= "event_type\":\"alert\"" | json | line_format "{{.alert_signature}}"'`
- `--addr` is the servers address
- `--limit=50` limits the amount of entry lines returned to 50
- Everything inside of `''` are filters
- `{job="suricata"}` filter by job
- `|=` is a pipeline filter in  logQL is substring. I read it as line must contain ...
- `"event_type\":\"alert\""` filters event type to be alerts
- `json` Parses lines as json
- `line_format "{{.alert_signature}}"` formats the output for us . 

After reading the output I founf our desired alert log: 
```
2025-11-24T10:38:18-05:00 {alert_category="", alert_rev="1", alert_severity="3", alert_signature="LAB UA hit", alert_signature_id="9900001", app_proto="http", dest_ip="23.192.228.84", dest_port="80", flow_bytes_toclient="1003", flow_bytes_toserver="350", flow_dest_ip="23.192.228.84", flow_dest_port="80", flow_id="447290227804394", flow_pkts_toclient="3", flow_pkts_toserver="4", flow_src_port="33772", flow_start="2025-11-24T10:38:17.956110-0500", http_hostname="example.com", http_http_content_type="text/html", http_http_method="GET", http_http_user_agent="CPS-NETSEC-LAB", http_length="513", http_protocol="HTTP/1.1", http_status="200", http_url="/", proto="TCP", src_port="33772", timestamp="2025-11-24T10:38:18.136376-0500", tx_id="0"} LAB UA hit
```

As you see the last 3 words are our message we put in the alert. 

Now lets find the latest source ip's from the last 5 minutes:

`logcli query --addr=http://localhost:3100 --limit=1000 --since=5m '{job="suricata"} |= "event_type\":\"alert\"" | json | line_format " {{.src_ip}} "' | sort | uniq -c | sort -nr | head` 

This makes it real easy to find the ip address of people pining our server/ network. If we can get their IP we can do a lot more. Here are 2 logs from my output:

```
1 2025-11-24T10:38:18-05:00 {alert_category="", alert_signature="LAB UA hit", alert_signature_id="9900001", app_proto="http", dest_ip="23.192.228.84", dest_port="80", flow_bytes_toclient="1003", flow_bytes_toserver="350", flow_dest_ip="23.192.228.84", flow_dest_port="80", flow_id="447290227804394", flow_pkts_toclient="3", flow_pkts_toserver="4", flow_src_port="33772", flow_start="2025-11-24T10:38:17.956110-0500", http_hostname="example.com", http_http_content_type="text/html", http_http_method="GET", http_http_user_agent="CPS-NETSEC-LAB", http_length="513", http_protocol="HTTP/1.1", http_status="200", http_url="/", proto="TCP", src_port="33772", timestamp="2025-11-24T10:38:18.136376-0500", tx_id="0"} 192.168.1.95

1 2025-11-24T10:37:43-05:00 {alert_category="Not Suspicious Traffic", alert_signature="ET INFO Spotify P2P Client", alert_signature_id="2027397", app_proto="failed", dest_ip="192.168.1.255", dest_port="57621", flow_bytes_toclient="0", flow_bytes_toserver="3526", flow_dest_ip="192.168.1.255", flow_dest_port="57621", flow_id="2244064587123700", flow_pkts_toclient="0", flow_pkts_toserver="41", flow_src_port="57621", flow_start="2025-11-24T10:17:43.391415-0500", proto="UDP", src_port="57621", timestamp="2025-11-24T10:37:43.412749-0500"}                                                                                                                                                                            192.168.1.95
1 2025-11-24T10:37:13-05:00 {alert_category="Not Suspicious Traffic", alert_signature="ET INFO Spotify P2P Client", alert_signature_id="2027397", app_proto="failed", dest_ip="192.168.1.255", dest_port="57621", flow_bytes_toclient="0", flow_bytes_toserver="46784", flow_dest_ip="192.168.1.255", flow_dest_port="57621", flow_id="1972984928917134", flow_pkts_toclient="0", flow_pkts_toserver="544", flow_src_port="57621", flow_start="2025-11-24T06:05:43.000619-0500", proto="UDP", src_port="57621", timestamp="2025-11-24T10:37:13.412207-0500"}

192.168.1.95
```
From this we can see that we are only getting pinged by ourselves from spotify and our curl request. But this is very useful for a SOC because it can give them a trail to follow back to the culprit if an event occurs, but also can act as a deterrent for attackers because they don't want to get caught. 

Now lets add and test another rule! To do so just append another rule to the <u>/etc/suricata/rules/local.rules</u> such as:

`alert ssh any any -> $HOME_NET 22 (msg:"SSH Connection Attempt Detected"; flow:to_server,established; threshold: type limit, track by_src, count 1, seconds 60; classtype:misc-activity; sid:1000001; rev:1;)`

This rule detects any ssh attempt connections.

Then restart suricata and check your rules syntax:

```
sudo systemctl restart suricata; 
sudo suricata -T -c /etc/suricata/suricata.yaml -v
```

To verify everthing worked I made a few ssh connections from my laptop to the host machine then ran:

`logcli query --addr=http://localhost:3100 --limit=50 --since=1h -o raw '{job="suricata"} |= "alert" |= "SSH" | json | line_format "{{.alert_signature}} | {{.src_ip}} -> {{.dest_ip}}"'`
Same command structure as before but 
- `--since` limits the quereies from the previous time specified in this case 1 hour
- `-o raw` what an output format that I prefered suprisingly
- Then I fileted by suricata logs, alerts, contains "SSH" 
- Then formatted everything to be readable the commands json and foward

My output looked like:
```
2025/11/26 12:38:26 http://localhost:3100/loki/api/v1/query_range?direction=BACKWARD&end=1764178706076659000&limit=50&query=%7Bjob%3D%22suricata%22%7D+%7C%3D+%22alert%22+%7C%3D+%22SSH%22+%7C+json+%7C+line_format+%22%7B%7B.alert_signature%7D%7D+%7C+%7B%7B.src_ip%7D%7D+-%3E+%7B%7B.dest_ip%7D%7D%22&start=1764175106076659000
2025/11/26 12:38:26 Common labels: {alert_action="allowed", alert_gid="1", app_proto="ssh", event_type="alert", filename="/var/log/suricata/eve.json", flow_dest_ip="192.168.1.95", flow_dest_port="22", flow_id="1115511291635426", flow_src_ip="68.193.96.196", flow_src_port="54732", flow_start="2025-11-26T12:31:07.325261-0500", in_iface="enp9s0", job="suricata", pkt_src="wire/pcap", proto="TCP", ssh_client_proto_version="2.0", ssh_client_software_version="OpenSSH_9.9", ssh_server_proto_version="2.0", ssh_server_software_version="OpenSSH_9.6p1"}
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
SSH Connection Attempt - 192.168.1.95 | 192.168.1.95 -> 68.193.96.196
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
ALERT: Multiple SSH Connection Attempts - Possible Brute Force | 68.193.96.196 -> 192.168.1.95
SSH Connection Attempt - 192.168.1.95 | 192.168.1.95 -> 68.193.96.196
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
SSH Connection Attempt - 192.168.1.95 | 192.168.1.95 -> 68.193.96.196
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
SSH Connection Attempt - 192.168.1.95 | 192.168.1.95 -> 68.193.96.196
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
SSH Connection Attempt - 192.168.1.95 | 192.168.1.95 -> 68.193.96.196
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
SSH Connection Attempt - 192.168.1.95 | 192.168.1.95 -> 68.193.96.196
SSH Connection Attempt - 192.168.1.95 | 68.193.96.196 -> 192.168.1.95
```
To make this rule more specific I'd edit the rules to detect failed login attempts and successful attempts rather than just the ping. This is important because if this were a larger scale and our logs were litered with false positives, the true positives are more likely to slip through because of unattentional blindness. 

Now to clean everything up if needed:

```
sudo docker stop promtail loki;
sudo docker rm promtail loki; 
sudo apt purge -y suricata;
sudo docker prune system prune -a -f
```
- Command 1 stops the containers from running
- Command 2 removes their image from memory
- Command 3 removes suricata from your host
- Command 4 removes all other versions and dangling images and stopped containers from your system


So in this session we assembled a SIEM (Security Info and Event Management), with the use of 3 components loki, promtail, and suricata. We were able to have end to end detection with logging. This is a great skill to have especially if you're going to manage a server, we get to know whats going on, find what we want to find, and are able to deal with special circumstances thanks to the flexibility of our components.