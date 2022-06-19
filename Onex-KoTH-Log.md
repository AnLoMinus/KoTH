 
---
 
# Anlominus KoTH Report for Onex 
#### Date: Sun Jun 19 20:49:02 IDT 2022
 
---
 
# 📜 Menu

      [a] - Anonymity Surfing
      [1] - Planning and Scoping
      [2] - Reconnaissance & Vulnerability Assessment
      [3] - Gaining Access & Maintaining Access
      [4] - Covering tracks
      [5] - Analysis & Reporting

      ┌──[ Anlominus 👽 KoTH $~]
      └──╼
      
 
---
#### Date: Sun Jun 19 20:49:02 IDT 2022
 
# [1] - Planning and Scoping 
### Planning Log 1.1.1.1: 
 
---
#### Date: Sun Jun 19 20:50:04 IDT 2022
 
# [2] - Reconnaissance & Vulnerability Assessment 
 
### Arp Scan Log 1.1.1.1: 
 
 
 ? (192.168.43.1) at d8:63:75:9e:6f:fd on en0 ifscope [ethernet]
? (224.0.0.251) at 1:0:5e:0:0:fb on en0 ifscope permanent [ethernet]
? (239.255.255.250) at 1:0:5e:7f:ff:fa on en0 ifscope permanent [ethernet] 
 
### TraceRoute Scan Log 1.1.1.1: 
 
  1  * * *
 2  * * *
 3  10.224.224.233 (10.224.224.233)  116.388 ms  16.780 ms  78.710 ms
 4  10.224.224.110 (10.224.224.110)  46.690 ms  59.499 ms  39.083 ms
 5  * * *
 6  37.26.146.26 (37.26.146.26)  73.566 ms  87.380 ms  52.195 ms
 7  172.25.87.2 (172.25.87.2)  107.499 ms  41.917 ms  67.382 ms
 8  core1-v200-int-rt1.nta.nv.net.il (212.143.12.92)  52.855 ms
    core2-0-1-0-5-int-net-rt2.nta.nv.net.il (212.143.12.88)  52.664 ms
    core1-v200-int-rt1.nta.nv.net.il (212.143.12.92)  50.473 ms
 9  core1-0-1.hfa.nv.net.il (212.143.12.13)  69.150 ms
    core2-be1392.ory.nv.net.il (212.143.12.91)  55.498 ms
    core1-be1391.ory.nv.net.il (212.143.12.121)  48.441 ms
10  cdn1-22-core2.ory.nv.net.il (207.232.57.98)  49.263 ms
    cdn1-20-core1.ory.nv.net.il (207.232.57.94)  51.308 ms
    cdn1-22-core2.ory.nv.net.il (207.232.57.98)  52.423 ms
11  212.150.71.151 (212.150.71.151)  64.425 ms
    212.143.232.3 (212.143.232.3)  59.229 ms  86.077 ms
12  one.one.one.one (1.1.1.1)  54.100 ms  56.588 ms  64.712 ms 
 
### Ping Scan Log 1.1.1.1: 
 
 PING 1.1.1.1 (1.1.1.1): 56 data bytes
64 bytes from 1.1.1.1: icmp_seq=0 ttl=55 time=70.937 ms
64 bytes from 1.1.1.1: icmp_seq=1 ttl=55 time=69.923 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=55 time=63.117 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=55 time=59.647 ms

--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 59.647/65.906/70.937/4.701 ms 
 
### Dig Scan Log 1.1.1.1: 
 
 
; <<>> DiG 9.10.6 <<>> 1.1.1.1 all
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 23787
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;1.1.1.1.			IN	A

;; AUTHORITY SECTION:
.			82877	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2022061900 1800 900 604800 86400

;; Query time: 134 msec
;; SERVER: 2001:4860:4860::8888#53(2001:4860:4860::8888)
;; WHEN: Sun Jun 19 20:50:57 IDT 2022
;; MSG SIZE  rcvd: 111

;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 64081
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;all.				IN	A

;; AUTHORITY SECTION:
.			86143	IN	SOA	a.root-servers.net. nstld.verisign-grs.com. 2022061901 1800 900 604800 86400

;; Query time: 113 msec
;; SERVER: 2001:4860:4860::8888#53(2001:4860:4860::8888)
;; WHEN: Sun Jun 19 20:50:57 IDT 2022
;; MSG SIZE  rcvd: 107 
 
### Nslookup Scan Log 1.1.1.1: 
 
 Server:		2001:4860:4860::8888
Address:	2001:4860:4860::8888#53

Non-authoritative answer:
1.1.1.1.in-addr.arpa	name = one.one.one.one.

Authoritative answers can be found from: 
 
### WhoIs Scan Log 1.1.1.1: 
 
 % IANA WHOIS server
% for more information on IANA, visit http://www.iana.org
% This query returned 1 object

refer:        whois.apnic.net

inetnum:      1.0.0.0 - 1.255.255.255
organisation: APNIC
status:       ALLOCATED

whois:        whois.apnic.net

changed:      2010-01
source:       IANA

# whois.apnic.net

% [whois.apnic.net]
% Whois data copyright terms    http://www.apnic.net/db/dbcopyright.html

% Information related to '1.1.1.0 - 1.1.1.255'

% Abuse contact for '1.1.1.0 - 1.1.1.255' is 'helpdesk@apnic.net'

inetnum:        1.1.1.0 - 1.1.1.255
netname:        APNIC-LABS
descr:          APNIC and Cloudflare DNS Resolver project
descr:          Routed globally by AS13335/Cloudflare
descr:          Research prefix for APNIC Labs
country:        AU
org:            ORG-ARAD1-AP
admin-c:        AR302-AP
tech-c:         AR302-AP
abuse-c:        AA1412-AP
status:         ASSIGNED PORTABLE
remarks:        ---------------
remarks:        All Cloudflare abuse reporting can be done via
remarks:        resolver-abuse@cloudflare.com
remarks:        ---------------
mnt-by:         APNIC-HM
mnt-routes:     MAINT-AU-APNIC-GM85-AP
mnt-irt:        IRT-APNICRANDNET-AU
last-modified:  2020-07-15T13:10:57Z
source:         APNIC

irt:            IRT-APNICRANDNET-AU
address:        PO Box 3646
address:        South Brisbane, QLD 4101
address:        Australia
e-mail:         helpdesk@apnic.net
abuse-mailbox:  helpdesk@apnic.net
admin-c:        AR302-AP
tech-c:         AR302-AP
auth:           # Filtered
remarks:        helpdesk@apnic.net was validated on 2021-02-09
mnt-by:         MAINT-AU-APNIC-GM85-AP
last-modified:  2021-03-09T01:10:21Z
source:         APNIC

organisation:   ORG-ARAD1-AP
org-name:       APNIC Research and Development
country:        AU
address:        6 Cordelia St
phone:          +61-7-38583100
fax-no:         +61-7-38583199
e-mail:         helpdesk@apnic.net
mnt-ref:        APNIC-HM
mnt-by:         APNIC-HM
last-modified:  2017-10-11T01:28:39Z
source:         APNIC

role:           ABUSE APNICRANDNETAU
address:        PO Box 3646
address:        South Brisbane, QLD 4101
address:        Australia
country:        ZZ
phone:          +000000000
e-mail:         helpdesk@apnic.net
admin-c:        AR302-AP
tech-c:         AR302-AP
nic-hdl:        AA1412-AP
remarks:        Generated from irt object IRT-APNICRANDNET-AU
abuse-mailbox:  helpdesk@apnic.net
mnt-by:         APNIC-ABUSE
last-modified:  2021-03-09T01:10:22Z
source:         APNIC

role:           APNIC RESEARCH
address:        PO Box 3646
address:        South Brisbane, QLD 4101
address:        Australia
country:        AU
phone:          +61-7-3858-3188
fax-no:         +61-7-3858-3199
e-mail:         research@apnic.net
nic-hdl:        AR302-AP
tech-c:         AH256-AP
admin-c:        AH256-AP
mnt-by:         MAINT-APNIC-AP
last-modified:  2018-04-04T04:26:04Z
source:         APNIC

% Information related to '1.1.1.0/24AS13335'

route:          1.1.1.0/24
origin:         AS13335
descr:          APNIC Research and Development
                6 Cordelia St
mnt-by:         MAINT-AU-APNIC-GM85-AP
last-modified:  2018-03-16T16:58:06Z
source:         APNIC

% This query was served by the APNIC Whois Service version 1.88.16 (WHOIS-UK4) 
 
### Dirb Scan Log 1.1.1.1: 
 
  
 
### Nmap Scan Log 1.1.1.1: 
 
  
 
---
 
 
