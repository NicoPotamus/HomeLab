# Firewall

`sudo ufw status` - self explanatory; also good for verifying if its downloaded

`sudo ufw allow 22/tcp` - Allow ssh; Good to allow this before enabling firewall beacuse if you are doing this via ssh you'll get shut out. 

`sudo ss -tuln` - Check the other ports that are open that you may need to allow

`lsof -i :<PORT NUMBER>` get info on specfiic port

`sudo ufw status verbose` - get actual info on system

Sample output
    
    Status: active
    Logging: on (low)
    Default: deny (incoming), allow (outgoing), disabled (routed)
    New profiles: skip

    To                         Action      From
    --                         ------      ----
    22/tcp                     ALLOW IN    Anywhere                  
    22/tcp (v6)                ALLOW IN    Anywhere (v6)             

`sudo ufw deny from 10.0.0.0` - deny profiles 

`sudo ufw allow from 192.168.1.50 to any port 587` - allow a certain ip to one port on system (Simple Mail Transfer Protocol Port)

`sudo ufw status verbose` output:

    Status: active
    Logging: on (low)
    Default: deny (incoming), allow (outgoing), disabled (routed)
    New profiles: skip

    To                         Action      From
    --                         ------      ----
    22/tcp                     ALLOW IN    Anywhere                  
    Anywhere                   DENY IN     10.0.0.0                  
    587                        ALLOW IN    192.168.1.50              
    22/tcp (v6)                ALLOW IN    Anywhere (v6)             

`sudo ufw logging on` - enable system logging

`sudo ufw logging high` - set logging level

- low: Minimal logging, mainly for blocked incoming packets.
- medium: Includes blocked incoming packets with additional packet header
details.
- high: Includes all blocked packets and connection information.
- full: Extensive logging of all UFW events

`sudo tail -f /var/log/ufw.log` - view logs for system
- `-f` - provides live logging
    
```
2025-10-04T00:27:14.584939-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW AUDIT] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=86 TOS=0x00 PREC=0x00 TTL=64 ID=26904 PROTO=UDP SPT=59247 DPT=53 LEN=66 
2025-10-04T00:27:14.584978-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW ALLOW] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=86 TOS=0x00 PREC=0x00 TTL=64 ID=26904 PROTO=UDP SPT=59247 DPT=53 LEN=66 
2025-10-04T00:27:14.612474-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW AUDIT] IN=enp1s0 OUT= MAC=52:54:00:04:ad:1e:52:54:00:cd:e1:0a:08:00 SRC=192.168.122.1 DST=192.168.122.34 LEN=422 TOS=0x00 PREC=0x00 TTL=64 ID=63435 DF PROTO=UDP SPT=53 DPT=59247 LEN=402 
2025-10-04T00:27:26.264046-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW AUDIT] IN=enp1s0 OUT= MAC=01:00:5e:00:00:fb:52:54:00:cd:e1:0a:08:00 SRC=192.168.122.1 DST=224.0.0.251 LEN=113 TOS=0x00 PREC=0x00 TTL=1 ID=48817 DF PROTO=UDP SPT=5353 DPT=5353 LEN=93 
2025-10-04T00:28:44.309376-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW AUDIT] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=337 TOS=0x00 PREC=0x00 TTL=64 ID=58797 DF PROTO=UDP SPT=68 DPT=67 LEN=317 
2025-10-04T00:28:44.309440-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW ALLOW] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=337 TOS=0x00 PREC=0x00 TTL=64 ID=58797 DF PROTO=UDP SPT=68 DPT=67 LEN=317 
```

`sudo cat /var/log/ufw.log | grep "ALLOW"` - find all occurances of what made it through firewall. No output for DENY which is good. I assume because I'm doing thiso n a vm and I just enabled logging.

    2025-10-04T00:27:14.584978-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW ALLOW] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=86 TOS=0x00 PREC=0x00 TTL=64 ID=26904 PROTO=UDP SPT=59247 DPT=53 LEN=66 
    2025-10-04T00:28:44.309440-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW ALLOW] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=337 TOS=0x00 PREC=0x00 TTL=64 ID=58797 DF PROTO=UDP SPT=68 DPT=67 LEN=317 
    2025-10-04T00:28:44.486072-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW ALLOW] IN= OUT=enp1s0 SRC=192.168.122.34 DST=192.168.122.1 LEN=86 TOS=0x00 PREC=0x00 TTL=64 ID=15687 PROTO=UDP SPT=59371 DPT=53 LEN=66 
    2025-10-04T00:28:44.516086-04:00 nicod-Standard-PC-Q35-ICH9-2009 kernel: [UFW ALLOW] IN= OUT=enp1s0 SRC=192.168.122.34 DST=185.125.190.18 LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=63076 DF PROTO=TCP SPT=44408 DPT=80 WINDOW=64240 RES=0x00 SYN URGP=0 
