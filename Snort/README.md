# SNORT
---
This lab was a bit opf a doozy to get going, my vm couldn't find the package. I failed on 2 different occassions to build the program from it's source repo, for version 3 and 2.9 even with the use of ai and forums. Then I resorted to using my tower running ubuntu. 

`sudo apt install snort -y` install snort

install some community rules
```
sudo wget https://www.snort.org/downloads/community/community-rules.tar.gz
sudo tar -xvzf community-rules.tar.gz
sudo cp community-rules/* /etc/snort/rules/
```
A rule file that sticks out to me is ddos.rules, I belive this files contains alerts to log any potential ddos attacks along with courses of action if things progress (ie dropping a connection). The rule file is a set of intructions to detect and or deal with malciious activity. 


running snort with `snort -T -c /etc/snort/snort.conf`

```
4058 Snort rules read
    3384 detection rules
    0 decoder rules
    0 preprocessor rules
3384 Option Chains linked into 932 Chain Headers
+++++++++++++++++++++++++++++++++++++++++++++++++++

+-------------------[Rule Port Counts]---------------------------------------
|             tcp     udp    icmp      ip
|     src     151      18       0       0
|     dst    3306     126       0       0
|     any     383      48      53      22
|      nc      27       8      16      20
|     s+d      12       5       0       0
+----------------------------------------------------------------------------

+-----------------------[detection-filter-config]------------------------------
| memory-cap : 1048576 bytes
+-----------------------[detection-filter-rules]-------------------------------
| none
-------------------------------------------------------------------------------

+-----------------------[rate-filter-config]-----------------------------------
| memory-cap : 1048576 bytes
+-----------------------[rate-filter-rules]------------------------------------
| none
-------------------------------------------------------------------------------

+-----------------------[event-filter-config]----------------------------------
| memory-cap : 1048576 bytes
+-----------------------[event-filter-global]----------------------------------
| none
+-----------------------[event-filter-local]-----------------------------------
| gen-id=1      sig-id=2924       type=Threshold tracking=dst count=10  seconds=60 
| gen-id=1      sig-id=1991       type=Limit     tracking=src count=1   seconds=60 
| gen-id=1      sig-id=2523       type=Both      tracking=dst count=10  seconds=10 
| gen-id=1      sig-id=2494       type=Both      tracking=dst count=20  seconds=60 
| gen-id=1      sig-id=2923       type=Threshold tracking=dst count=10  seconds=60 
| gen-id=1      sig-id=2495       type=Both      tracking=dst count=20  seconds=60 
| gen-id=1      sig-id=2496       type=Both      tracking=dst count=20  seconds=60 
| gen-id=1      sig-id=2275       type=Threshold tracking=dst count=5   seconds=60 
| gen-id=1      sig-id=3273       type=Threshold tracking=src count=5   seconds=2  
| gen-id=1      sig-id=3152       type=Threshold tracking=src count=5   seconds=2  
+-----------------------[suppression]------------------------------------------
| none
-------------------------------------------------------------------------------
Rule application order: pass->drop->sdrop->reject->alert->log
Verifying Preprocessor Configurations!
WARNING: flowbits key 'smb.tree.create.llsrpc' is set but not ever checked.
WARNING: flowbits key 'ms_sql_seen_dns' is checked but not ever set.
33 out of 1024 flowbits in use.

MaxRss at the end of rules:60608

[ Port Based Pattern Matching Memory ]
+- [ Aho-Corasick Summary ] -------------------------------------
| Storage Format    : Full-Q 
| Finite Automaton  : DFA
| Alphabet Size     : 256 Chars
| Sizeof State      : Variable (1,2,4 bytes)
| Instances         : 215
|     1 byte states : 204
|     2 byte states : 11
|     4 byte states : 0
| Characters        : 64755
| States            : 31951
| Transitions       : 863868
| State Density     : 10.6%
| Patterns          : 5041
| Match States      : 3836
| Memory (MB)       : 16.90
|   Patterns        : 0.51
|   Match Lists     : 1.01
|   DFA
|     1 byte states : 1.02
|     2 byte states : 13.96
|     4 byte states : 0.00
+----------------------------------------------------------------
[ Number of patterns truncated to 20 bytes: 1038 ]

MaxRss at the end of detection rules:104892

        --== Initialization Complete ==--

   ,,_     -*> Snort! <*-
  o"  )~   Version 2.9.20 GRE (Build 82) 
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team
           Copyright (C) 2014-2022 Cisco and/or its affiliates. All rights reserved.
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.
           Using libpcap version 1.10.4 (with TPACKET_V3)
           Using PCRE version: 8.39 2016-06-14
           Using ZLIB version: 1.3

           Rules Engine: SF_SNORT_DETECTION_ENGINE  Version 3.2  <Build 1>
           Preprocessor Object: SF_SIP  Version 1.1  <Build 1>
           Preprocessor Object: SF_S7COMMPLUS  Version 1.0  <Build 1>
           Preprocessor Object: SF_FTPTELNET  Version 1.2  <Build 13>
           Preprocessor Object: SF_IMAP  Version 1.0  <Build 1>
           Preprocessor Object: SF_SSH  Version 1.1  <Build 3>
           Preprocessor Object: appid  Version 1.1  <Build 5>
           Preprocessor Object: SF_MODBUS  Version 1.1  <Build 1>
           Preprocessor Object: SF_POP  Version 1.0  <Build 1>
           Preprocessor Object: SF_SSLPP  Version 1.1  <Build 4>
           Preprocessor Object: SF_SDF  Version 1.1  <Build 1>
           Preprocessor Object: SF_DNS  Version 1.1  <Build 4>
           Preprocessor Object: SF_DCERPC2  Version 1.0  <Build 3>
           Preprocessor Object: SF_GTP  Version 1.1  <Build 1>
           Preprocessor Object: SF_SMTP  Version 1.1  <Build 9>
           Preprocessor Object: SF_DNP3  Version 1.1  <Build 1>
           Preprocessor Object: SF_REPUTATION  Version 1.1  <Build 1>

Total snort Fixed Memory Cost - MaxRss:104892
Snort successfully validated the configuration!
Snort exiting

```
---
## Run Snort in IDS (detection)

`sudo snort -c /etc/snort/snort.conf -i eth0` 

output, there are still dependency errors but since i've been toying with only the install for 2 hours we're going to keep pushing along

when taking a peek at the logs I found only one file called 'snort.alert.fast'
I believe this file is here because of the rules we put in place before in the local.rules file. Here is a sample of the alert file 
```
11/01-23:15:44.153842  [**] [1:1384:8] MISC UPnP malformed advertisement [**] [Classification: Misc Attack] [Priority: 2] {UDP} 192.168.1.1:1900 -> 239.255.255.250:1900
11/01-23:15:44.161107  [**] [1:1384:8] MISC UPnP malformed advertisement [**] [Classification: Misc Attack] [Priority: 2] {UDP} 192.168.1.1:1900 -> 239.255.255.250:1900
11/01-23:15:44.162524  [**] [1:1384:8] MISC UPnP malformed advertisement [**] [Classification: Misc Attack] [Priority: 2] {UDP} 192.168.1.1:1900 -> 239.255.255.250:1900
11/01-23:15:44.165518  [**] [1:1384:8] MISC UPnP malformed advertisement [**] [Classification: Misc Attack] [Priority: 2] {UDP} 192.168.1.1:1900 -> 239.255.255.250:1900

```


to run snort as a Daemon (background process) all I have to do is run 
`sudo snort -D -c /etc/snort/snort.conf`
use the `top` command to verify

To kill the snort process all you would have to do is kill the process id of snort. This will stop any current execution ie `kill 9956` if snorts pid was 9956
