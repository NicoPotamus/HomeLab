# Identify any weaknesses in System

## `ip addr` ; `ifconfig`
- Give same response (ip a  is colorized; ifconfig is neater)
- Show protocol (IP or IPv6) address on a device.
- ifconfig is depraceted; stop using it and use `ip addr`

My Output from `ifconfig`:

```
enp1s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.122.214  netmask 255.255.255.0  broadcast 192.168.122.255
        inet6 fe80::5054:ff:fe6a:290f  prefixlen 64  scopeid 0x20<link>
        ether 52:54:00:6a:29:0f  txqueuelen 1000  (Ethernet)
        RX packets 9154  bytes 58493804 (58.4 MB)
        RX errors 0  dropped 1781  overruns 0  frame 0
        TX packets 7066  bytes 582500 (582.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 428  bytes 46154 (46.1 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 428  bytes 46154 (46.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0 
```

## `netstat` or `ss`
- ss offers more information
- Used to get port information 
### Flags:
- `-t` output TCP
- `-u` output udp
- `-l` output ports listening
- `-n` output state without resolving names

Output from `ss -tuln`
```
Netid           State             Recv-Q            Send-Q                       Local Address:Port                        Peer Address:Port           
udp             UNCONN            0                 0                                  0.0.0.0:55907                            0.0.0.0:*              
udp             UNCONN            0                 0                                  0.0.0.0:5353                             0.0.0.0:*              
udp             UNCONN            0                 0                               127.0.0.54:53                               0.0.0.0:*              
udp             UNCONN            0                 0                            127.0.0.53%lo:53                               0.0.0.0:*              
udp             UNCONN            0                 0                                     [::]:51750                               [::]:*              
udp             UNCONN            0                 0                                     [::]:5353                                [::]:*              
tcp             LISTEN            0                 4096                             127.0.0.1:631                              0.0.0.0:*              
tcp             LISTEN            0                 4096                         127.0.0.53%lo:53                               0.0.0.0:*              
tcp             LISTEN            0                 4096                            127.0.0.54:53                               0.0.0.0:*              
tcp             LISTEN            0                 4096                                 [::1]:631                                 [::]:*    
```

## `lsof`
- Acronym for list(ls) open(o) files(f)
- Used to get all network connections 
### Flags:
- `-i` Output network files
- `-P` -n Prevent resolution of names associated making the command faster and more ledgible

Output from `lsof -i -P -n`
``` 
COMMAND    PID            USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
systemd-r 1675 systemd-resolve   14u  IPv4  16721      0t0  UDP 127.0.0.53:53 
systemd-r 1675 systemd-resolve   15u  IPv4  16722      0t0  TCP 127.0.0.53:53 (LISTEN)
systemd-r 1675 systemd-resolve   16u  IPv4  16723      0t0  UDP 127.0.0.54:53 
systemd-r 1675 systemd-resolve   17u  IPv4  16724      0t0  TCP 127.0.0.54:53 (LISTEN)
avahi-dae 1929           avahi   12u  IPv4   7416      0t0  UDP *:5353 
avahi-dae 1929           avahi   13u  IPv6   7417      0t0  UDP *:5353 
avahi-dae 1929           avahi   14u  IPv4   7418      0t0  UDP *:55907 
avahi-dae 1929           avahi   15u  IPv6   7419      0t0  UDP *:51750 
NetworkMa 2068            root   26u  IPv4   9563      0t0  UDP 192.168.122.214:68->192.168.122.1:67 
cupsd     2245            root    6u  IPv6   6563      0t0  TCP [::1]:631 (LISTEN)
cupsd     2245            root    7u  IPv4   6564      0t0  TCP 127.0.0.1:631 (LISTEN)
```

## `nmap`
- Port Scanner Features
- Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what
    - services (application name and version) those hosts are offering,
    - operating systems (and OS versions) they are running,
    - packet filters/firewalls are in use, and dozens of other characteristics. While
- Nmap is commonly used for 
    - security audits,
    - network inventory
    - managing service upgrade schedules 
    - monitoring host or service uptime.
### Flags:
- `-sS` performs a stealth TCP SYN scan 
- `-O` attempts to determine the operating system of the target
- `-sP` option in Nmap is a Ping Scan
    - Discovers which hosts on a network are up without performing a port scan
- `-sV` enables version detection
    - provides detailed information about the services running on open ports
- `-script vuln` runs scripts that check for various vulnerabilities

Output `nmap -sS -O localhost`
- Scans Network
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-25 10:34 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000073s latency).
Not shown: 999 closed tcp ports (reset)
PORT    STATE SERVICE
631/tcp open  ipp
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6.32
OS details: Linux 2.6.32
Network Distance: 0 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1.73 seconds
```
Output `nmap -sP 192.168.1.0/24`
- Check open ports on a servers network
- Identifies all live hosts on your local network
- This helps you understand the devices present in your network
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-25 10:39 EDT
Nmap scan report for Docsis-Gateway (192.168.1.1)
Host is up (0.0065s latency).
Nmap scan report for iPhone (192.168.1.45)
Host is up (0.090s latency).
Nmap scan report for fedora (192.168.1.200)
Host is up (0.0015s latency).
Nmap scan report for LGwebOSTV (192.168.1.224)
Host is up (0.025s latency).
Nmap done: 256 IP addresses (4 hosts up) scanned in 4.93 seconds
```

Output `nmap -sV localhost`
- Scans for open ports 
- attempts to determine the service and version running on each port
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-25 10:39 EDT
Nmap scan report for Docsis-Gateway (192.168.1.1)
Host is up (0.0065s latency).
Nmap scan report for iPhone (192.168.1.45)
Host is up (0.090s latency).
Nmap scan report for fedora (192.168.1.200)
Host is up (0.0015s latency).
Nmap scan report for LGwebOSTV (192.168.1.224)
Host is up (0.025s latency).
Nmap done: 256 IP addresses (4 hosts up) scanned in 4.93 seconds
```

Output `nmap --script vuln localhost`
- identify known vulnerabilities on the server
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-25 10:46 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000050s latency).
Not shown: 999 closed tcp ports (reset)
PORT    STATE SERVICE
631/tcp open  ipp
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
|_ssl-ccs-injection: No reply from server (TIMEOUT)
| http-method-tamper: 
|   VULNERABLE:
|   Authentication bypass by HTTP verb tampering
|     State: VULNERABLE (Exploitable)
|       This web server contains password protected resources vulnerable to authentication bypass
|       vulnerabilities via HTTP verb tampering. This is often found in web servers that only limit access to the
|        common HTTP methods and in misconfigured .htaccess files.
|              
|     Extra information:
|       
|   URIs suspected to be vulnerable to HTTP verb tampering:
|     /admin [GENERIC]
|   
|     References:
|       https://www.owasp.org/index.php/Testing_for_HTTP_Methods_and_XST_%28OWASP-CM-008%29
|       http://capec.mitre.org/data/definitions/274.html
|       http://www.mkit.com.ar/labs/htexploit/
|_      http://www.imperva.com/resources/glossary/http_verb_tampering.html
| http-enum: 
|   /admin.php: Possible admin folder (401 Unauthorized)
|   /admin/: Possible admin folder (401 Unauthorized)
|   /admin/admin/: Possible admin folder (401 Unauthorized)
|   /administrator/: Possible admin folder (401 Unauthorized)
|   /adminarea/: Possible admin folder (401 Unauthorized)
|   /adminLogin/: Possible admin folder (401 Unauthorized)
|   /admin_area/: Possible admin folder (401 Unauthorized)
|   /administratorlogin/: Possible admin folder (401 Unauthorized)
|   /admin/account.php: Possible admin folder (401 Unauthorized)
|   /admin/index.php: Possible admin folder (401 Unauthorized)
|   /admin/login.php: Possible admin folder (401 Unauthorized)
|   /admin/admin.php: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.php: Possible admin folder (401 Unauthorized)
|   /admin_area/login.php: Possible admin folder (401 Unauthorized)
|   /admin/index.html: Possible admin folder (401 Unauthorized)
|   /admin/login.html: Possible admin folder (401 Unauthorized)
|   /admin/admin.html: Possible admin folder (401 Unauthorized)
|   /admin_area/index.php: Possible admin folder (401 Unauthorized)
|   /admin/home.php: Possible admin folder (401 Unauthorized)
|   /admin_area/login.html: Possible admin folder (401 Unauthorized)
|   /admin_area/index.html: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.php: Possible admin folder (401 Unauthorized)
|   /admincp/: Possible admin folder (401 Unauthorized)
|   /admincp/index.asp: Possible admin folder (401 Unauthorized)
|   /admincp/index.html: Possible admin folder (401 Unauthorized)
|   /admincp/login.php: Possible admin folder (401 Unauthorized)
|   /admin/account.html: Possible admin folder (401 Unauthorized)
|   /adminpanel.html: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.html: Possible admin folder (401 Unauthorized)
|   /admin_login.html: Possible admin folder (401 Unauthorized)
|   /admin/cp.php: Possible admin folder (401 Unauthorized)
|   /administrator/index.php: Possible admin folder (401 Unauthorized)
|   /administrator/login.php: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.php: Possible admin folder (401 Unauthorized)
|   /admin_login.php: Possible admin folder (401 Unauthorized)
|   /administrator/account.php: Possible admin folder (401 Unauthorized)
|   /administrator.php: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.html: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.php: Possible admin folder (401 Unauthorized)
|   /admin-login.php: Possible admin folder (401 Unauthorized)
|   /admin/home.html: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.html: Possible admin folder (401 Unauthorized)
|   /admin-login.html: Possible admin folder (401 Unauthorized)
|   /admincontrol.php: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.html: Possible admin folder (401 Unauthorized)
|   /adminLogin.html: Possible admin folder (401 Unauthorized)
|   /adminarea/index.html: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.html: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.html: Possible admin folder (401 Unauthorized)
|   /admin.html: Possible admin folder (401 Unauthorized)
|   /admin/cp.html: Possible admin folder (401 Unauthorized)
|   /adminpanel.php: Possible admin folder (401 Unauthorized)
|   /administrator/index.html: Possible admin folder (401 Unauthorized)
|   /administrator/login.html: Possible admin folder (401 Unauthorized)
|   /administrator/account.html: Possible admin folder (401 Unauthorized)
|   /administrator.html: Possible admin folder (401 Unauthorized)
|   /adminarea/login.html: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.html: Possible admin folder (401 Unauthorized)
|   /admincontrol.html: Possible admin folder (401 Unauthorized)
|   /adminLogin.php: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.php: Possible admin folder (401 Unauthorized)
|   /adminarea/index.php: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.php: Possible admin folder (401 Unauthorized)
|   /adminarea/login.php: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.php: Possible admin folder (401 Unauthorized)
|   /admin2.php: Possible admin folder (401 Unauthorized)
|   /admin2/login.php: Possible admin folder (401 Unauthorized)
|   /admin2/index.php: Possible admin folder (401 Unauthorized)
|   /administratorlogin.php: Possible admin folder (401 Unauthorized)
|   /admin/account.cfm: Possible admin folder (401 Unauthorized)
|   /admin/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin/login.cfm: Possible admin folder (401 Unauthorized)
|   /admin/admin.cfm: Possible admin folder (401 Unauthorized)
|   /admin.cfm: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.cfm: Possible admin folder (401 Unauthorized)
|   /admin_login.cfm: Possible admin folder (401 Unauthorized)
|   /adminpanel.cfm: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.cfm: Possible admin folder (401 Unauthorized)
|   /admincontrol.cfm: Possible admin folder (401 Unauthorized)
|   /admin/cp.cfm: Possible admin folder (401 Unauthorized)
|   /admincp/index.cfm: Possible admin folder (401 Unauthorized)
|   /admincp/login.cfm: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.cfm: Possible admin folder (401 Unauthorized)
|   /admin_area/login.cfm: Possible admin folder (401 Unauthorized)
|   /administrator/login.cfm: Possible admin folder (401 Unauthorized)
|   /administratorlogin.cfm: Possible admin folder (401 Unauthorized)
|   /administrator.cfm: Possible admin folder (401 Unauthorized)
|   /administrator/account.cfm: Possible admin folder (401 Unauthorized)
|   /adminLogin.cfm: Possible admin folder (401 Unauthorized)
|   /admin2/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin_area/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin2/login.cfm: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.cfm: Possible admin folder (401 Unauthorized)
|   /administrator/index.cfm: Possible admin folder (401 Unauthorized)
|   /adminarea/login.cfm: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.cfm: Possible admin folder (401 Unauthorized)
|   /adminarea/index.cfm: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.cfm: Possible admin folder (401 Unauthorized)
|   /admin-login.cfm: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.cfm: Possible admin folder (401 Unauthorized)
|   /admin/home.cfm: Possible admin folder (401 Unauthorized)
|   /admin/account.asp: Possible admin folder (401 Unauthorized)
|   /admin/index.asp: Possible admin folder (401 Unauthorized)
|   /admin/login.asp: Possible admin folder (401 Unauthorized)
|   /admin/admin.asp: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.asp: Possible admin folder (401 Unauthorized)
|   /admin_area/login.asp: Possible admin folder (401 Unauthorized)
|   /admin_area/index.asp: Possible admin folder (401 Unauthorized)
|   /admin/home.asp: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.asp: Possible admin folder (401 Unauthorized)
|   /admin.asp: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.asp: Possible admin folder (401 Unauthorized)
|   /admin-login.asp: Possible admin folder (401 Unauthorized)
|   /admin/cp.asp: Possible admin folder (401 Unauthorized)
|   /administrator/account.asp: Possible admin folder (401 Unauthorized)
|   /administrator.asp: Possible admin folder (401 Unauthorized)
|   /administrator/login.asp: Possible admin folder (401 Unauthorized)
|   /admincp/login.asp: Possible admin folder (401 Unauthorized)
|   /admincontrol.asp: Possible admin folder (401 Unauthorized)
|   /adminpanel.asp: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.asp: Possible admin folder (401 Unauthorized)
|   /admin_login.asp: Possible admin folder (401 Unauthorized)
|   /adminLogin.asp: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.asp: Possible admin folder (401 Unauthorized)
|   /adminarea/index.asp: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.asp: Possible admin folder (401 Unauthorized)
|   /adminarea/login.asp: Possible admin folder (401 Unauthorized)
|   /administrator/index.asp: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.asp: Possible admin folder (401 Unauthorized)
|   /admin2.asp: Possible admin folder (401 Unauthorized)
|   /admin2/login.asp: Possible admin folder (401 Unauthorized)
|   /admin2/index.asp: Possible admin folder (401 Unauthorized)
|   /administratorlogin.asp: Possible admin folder (401 Unauthorized)
|   /admin/account.aspx: Possible admin folder (401 Unauthorized)
|   /admin/index.aspx: Possible admin folder (401 Unauthorized)
|   /admin/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin/admin.aspx: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.aspx: Possible admin folder (401 Unauthorized)
|   /admin_area/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin_area/index.aspx: Possible admin folder (401 Unauthorized)
|   /admin/home.aspx: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.aspx: Possible admin folder (401 Unauthorized)
|   /admin.aspx: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.aspx: Possible admin folder (401 Unauthorized)
|   /admin-login.aspx: Possible admin folder (401 Unauthorized)
|   /admin/cp.aspx: Possible admin folder (401 Unauthorized)
|   /administrator/account.aspx: Possible admin folder (401 Unauthorized)
|   /administrator.aspx: Possible admin folder (401 Unauthorized)
|   /administrator/login.aspx: Possible admin folder (401 Unauthorized)
|   /admincp/index.aspx: Possible admin folder (401 Unauthorized)
|   /admincp/login.aspx: Possible admin folder (401 Unauthorized)
|   /admincontrol.aspx: Possible admin folder (401 Unauthorized)
|   /adminpanel.aspx: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.aspx: Possible admin folder (401 Unauthorized)
|   /admin_login.aspx: Possible admin folder (401 Unauthorized)
|   /adminLogin.aspx: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.aspx: Possible admin folder (401 Unauthorized)
|   /adminarea/index.aspx: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.aspx: Possible admin folder (401 Unauthorized)
|   /adminarea/login.aspx: Possible admin folder (401 Unauthorized)
|   /administrator/index.aspx: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin2.aspx: Possible admin folder (401 Unauthorized)
|   /admin2/login.aspx: Possible admin folder (401 Unauthorized)
|   /admin2/index.aspx: Possible admin folder (401 Unauthorized)
|   /administratorlogin.aspx: Possible admin folder (401 Unauthorized)
|   /admin/index.jsp: Possible admin folder (401 Unauthorized)
|   /admin/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin/admin.jsp: Possible admin folder (401 Unauthorized)
|   /admin_area/admin.jsp: Possible admin folder (401 Unauthorized)
|   /admin_area/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin_area/index.jsp: Possible admin folder (401 Unauthorized)
|   /admin/home.jsp: Possible admin folder (401 Unauthorized)
|   /admin/controlpanel.jsp: Possible admin folder (401 Unauthorized)
|   /admin.jsp: Possible admin folder (401 Unauthorized)
|   /admin/admin-login.jsp: Possible admin folder (401 Unauthorized)
|   /admin-login.jsp: Possible admin folder (401 Unauthorized)
|   /admin/cp.jsp: Possible admin folder (401 Unauthorized)
|   /administrator/account.jsp: Possible admin folder (401 Unauthorized)
|   /administrator.jsp: Possible admin folder (401 Unauthorized)
|   /administrator/login.jsp: Possible admin folder (401 Unauthorized)
|   /admincp/index.jsp: Possible admin folder (401 Unauthorized)
|   /admincp/login.jsp: Possible admin folder (401 Unauthorized)
|   /admincontrol.jsp: Possible admin folder (401 Unauthorized)
|   /admin/account.jsp: Possible admin folder (401 Unauthorized)
|   /adminpanel.jsp: Possible admin folder (401 Unauthorized)
|   /admin/admin_login.jsp: Possible admin folder (401 Unauthorized)
|   /admin_login.jsp: Possible admin folder (401 Unauthorized)
|   /adminLogin.jsp: Possible admin folder (401 Unauthorized)
|   /admin/adminLogin.jsp: Possible admin folder (401 Unauthorized)
|   /adminarea/index.jsp: Possible admin folder (401 Unauthorized)
|   /adminarea/admin.jsp: Possible admin folder (401 Unauthorized)
|   /adminarea/login.jsp: Possible admin folder (401 Unauthorized)
|   /administrator/index.jsp: Possible admin folder (401 Unauthorized)
|   /admincontrol/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin2.jsp: Possible admin folder (401 Unauthorized)
|   /admin2/login.jsp: Possible admin folder (401 Unauthorized)
|   /admin2/index.jsp: Possible admin folder (401 Unauthorized)
|   /administratorlogin.jsp: Possible admin folder (401 Unauthorized)
|   /admin1.php: Possible admin folder (401 Unauthorized)
|   /administr8.asp: Possible admin folder (401 Unauthorized)
|   /administr8.php: Possible admin folder (401 Unauthorized)
|   /administr8.jsp: Possible admin folder (401 Unauthorized)
|   /administr8.aspx: Possible admin folder (401 Unauthorized)
|   /administr8.cfm: Possible admin folder (401 Unauthorized)
|   /administr8/: Possible admin folder (401 Unauthorized)
|   /administer/: Possible admin folder (401 Unauthorized)
|   /administracao.php: Possible admin folder (401 Unauthorized)
|   /administracao.asp: Possible admin folder (401 Unauthorized)
|   /administracao.aspx: Possible admin folder (401 Unauthorized)
|   /administracao.cfm: Possible admin folder (401 Unauthorized)
|   /administracao.jsp: Possible admin folder (401 Unauthorized)
|   /administracion.php: Possible admin folder (401 Unauthorized)
|   /administracion.asp: Possible admin folder (401 Unauthorized)
|   /administracion.aspx: Possible admin folder (401 Unauthorized)
|   /administracion.jsp: Possible admin folder (401 Unauthorized)
|   /administracion.cfm: Possible admin folder (401 Unauthorized)
|   /administrators/: Possible admin folder (401 Unauthorized)
|   /adminpro/: Possible admin folder (401 Unauthorized)
|   /admins/: Possible admin folder (401 Unauthorized)
|   /admins.cfm: Possible admin folder (401 Unauthorized)
|   /admins.php: Possible admin folder (401 Unauthorized)
|   /admins.jsp: Possible admin folder (401 Unauthorized)
|   /admins.asp: Possible admin folder (401 Unauthorized)
|   /admins.aspx: Possible admin folder (401 Unauthorized)
|   /administracion-sistema/: Possible admin folder (401 Unauthorized)
|   /admin108/: Possible admin folder (401 Unauthorized)
|   /admin_cp.asp: Possible admin folder (401 Unauthorized)
|   /admin/backup/: Possible backup (401 Unauthorized)
|   /admin/download/backup.sql: Possible database backup (401 Unauthorized)
|   /robots.txt: Robots file
|   /admin/upload.php: Admin File Upload (401 Unauthorized)
|   /admin/CiscoAdmin.jhtml: Cisco Collaboration Server (401 Unauthorized)
|   /admin-console/: JBoss Console (401 Unauthorized)
|   /admin4.nsf: Lotus Domino (401 Unauthorized)
|   /admin5.nsf: Lotus Domino (401 Unauthorized)
|   /admin.nsf: Lotus Domino (401 Unauthorized)
|   /administrator/wp-login.php: Wordpress login page. (401 Unauthorized)
|   /admin/libraries/ajaxfilemanager/ajaxfilemanager.php: Log1 CMS (401 Unauthorized)
|   /admin/view/javascript/fckeditor/editor/filemanager/connectors/test.html: OpenCart/FCKeditor File upload (401 Unauthorized)
|   /admin/includes/tiny_mce/plugins/tinybrowser/upload.php: CompactCMS or B-Hind CMS/FCKeditor File upload (401 Unauthorized)
|   /admin/includes/FCKeditor/editor/filemanager/upload/test.html: ASP Simple Blog / FCKeditor File Upload (401 Unauthorized)
|   /admin/jscript/upload.php: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/jscript/upload.html: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/jscript/upload.pl: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/jscript/upload.asp: Lizard Cart/Remote File upload (401 Unauthorized)
|   /admin/environment.xml: Moodle files (401 Unauthorized)
|   /classes/: Potentially interesting folder
|   /es/: Potentially interesting folder
|   /help/: Potentially interesting folder
|_  /printers/: Potentially interesting folder

Nmap done: 1 IP address (1 host up) scanned in 48.81 seconds

```

## `tcpdump` 
- Inspect Network Traffic
- packet analyzer that captures and displays packet headers
of network traffic passing through a specified interface
## Flags:
 - `-i` `--interface` list of link-layer types, report the list of time stamp types, or report the results of compiling a filter expression on interface.

### The following was run on host system because NIC is unaccessible from VM(fedora)
Output `tcpdump -i wlp243s0`
- Monitors network traffic on a specific interface (e.g., eth0)
- Observe real-time traffic
```
dropped privs to tcpdump
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on wlp243s0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
10:56:31.999479 IP fedora.34328 > 209.205.228.50.ntp: NTPv4, Client, length 48
10:56:32.025290 IP fedora.57418 > _gateway.domain: 10538+ PTR? 50.228.205.209.in-addr.arpa. (45)
10:56:32.042987 IP _gateway.domain > fedora.57418: 10538 NXDomain 0/1/0 (104)
10:56:33.535455 ARP, Request who-has fedora tell _gateway, length 46
10:56:33.535480 ARP, Reply fedora is-at 52:d4:78:08:4e:2d (oui Unknown), length 28
10:56:33.943314 IP _gateway > all-systems.mcast.net: igmp query v2
10:56:33.999430 IP fedora.45541 > _gateway.domain: 34558+ PTR? 1.0.0.224.in-addr.arpa. (40)
10:56:34.020808 IP _gateway.domain > fedora.45541: 34558 1/0/0 PTR all-systems.mcast.net. (75)
10:56:34.211407 IP6 fedora.mdns > ff02::fb.mdns: 0 [7q] PTR (QM)? _ftp._tcp.local. PTR (QM)? _nfs._tcp.local. PTR (QM)? _afpovertcp._tcp.local. PTR (QM)? _smb._tcp.local. PTR (QM)? _sftp-ssh._tcp.local. PTR (QM)? _webdavs._tcp.local. PTR (QM)? _webdav._tcp.local. (118)
10:56:34.211578 IP fedora.mdns > mdns.mcast.net.mdns: 0 [7q] PTR (QM)? _ftp._tcp.local. PTR (QM)? _nfs._tcp.local. PTR (QM)? _afpovertcp._tcp.local. PTR (QM)? _smb._tcp.local. PTR (QM)? _sftp-ssh._tcp.local. PTR (QM)? _webdavs._tcp.local. PTR (QM)? _webdav._tcp.local. (118)
10:56:34.312852 IP fedora.55487 > _gateway.domain: 5012+ PTR? b.f.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.2.0.f.f.ip6.arpa. (90)
10:56:34.333320 IP _gateway.domain > fedora.55487: 5012 NXDomain 0/1/0 (154)
10:56:34.335402 IP fedora.41424 > _gateway.domain: 51356+ PTR? 251.0.0.224.in-addr.arpa. (42)
10:56:34.344352 IP fedora.38028 > LGwebOSTV.nvme-disc: Flags [P.], seq 2785468534:2785468651, ack 908127177, win 446, options [nop,nop,TS val 134813011 ecr 3735288096], length 117
10:56:34.348731 IP LGwebOSTV.nvme-disc > fedora.38028: Flags [P.], seq 1:118, ack 117, win 501, options [nop,nop,TS val 3735293106 ecr 134813011], length 117
10:56:34.348842 IP fedora.38028 > LGwebOSTV.nvme-disc: Flags [.], ack 118, win 446, options [nop,nop,TS val 134813016 ecr 3735293106], length 0
10:56:34.356075 IP _gateway.domain > fedora.41424: 51356 1/0/0 PTR mdns.mcast.net. (70)
10:56:34.416255 IP fedora.32812 > _gateway.domain: 33897+ PTR? 224.1.168.192.in-addr.arpa. (44)
10:56:34.419860 IP _gateway.domain > fedora.32812: 33897* 1/0/0 PTR LGwebOSTV. (67)
10:56:34.705383 IP fedora.35696 > LGwebOSTV.llmnr: Flags [S], seq 3290938037, win 64240, options [mss 1460,sackOK,TS val 134813372 ecr 0,nop,wscale 7,tfo  cookiereq,nop,nop], length 0
10:56:34.715886 IP LGwebOSTV.llmnr > fedora.35696: Flags [R.], seq 0, ack 3290938038, win 0, length 0
10:56:35.069080 IP LGwebOSTV > 239.255.255.250: igmp v2 report 239.255.255.250
10:56:35.143777 IP fedora.55746 > _gateway.domain: 8428+ PTR? 250.255.255.239.in-addr.arpa. (46)
10:56:35.147322 IP fedora.52464 > LGwebOSTV.nvme-disc: Flags [P.], seq 1019802073:1019802190, ack 990507163, win 449, options [nop,nop,TS val 134813814 ecr 3735288901], length 117
```
## `watch`
- runs a specified command at regular intervals

Output `-n 1 netstat -tulnp`
- Continuously monitors network connections, updating every second (-n 1). 
- Real-time observation of network activities, 
    - new connections 
    - services starting.
### Flags:
- `-n <Seconds>` update rate in seconds

Output `watch -n 1 netstat -tulnp`
- outputs a header stating the interval and command being run
- body of output from netstat

## `ufw`
- Uncomplicated Firewall
- front-end for managing iptables
- firewall configs

Output `ufw status verbose`
- The status verbose option provides a detailed view of the current firewall configuration
```
Status: inactive
```
Looks like I gotta set that up