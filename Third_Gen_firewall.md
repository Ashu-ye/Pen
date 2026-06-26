**https://pastebin.com/raw/d72VWsSc**



___________________________________________________________________________________________
IDS/IPS


What is a Intrusion Detection System?
`````````````````````````````````````
- An intrusion detection system (IDS) is a device or software application that monitors a network for malicious activity or policy violations. 

- Some IDS’s are capable of responding to detected intrusion upon discovery.

IDS Detection Types
````````````````````
+ Network intrusion detection systems (NIDS)
````````````````````````````````````````````
	- A system that analyzes incoming network traffic.

+ Host-based intrusion detection systems (HIDS)
```````````````````````````````````````````````
	- A system that monitors important operating system files.

+ Protocol-based Intrusion Detection System (PIDS):
```````````````````````````````````````````````````
	- It is trying to secure the web server by regularly monitoring the HTTPS protocol stream and accept the related HTTP protocol.

+ Application Protocol-based Intrusion Detection System (APIDS):
````````````````````````````````````````````````````````````````
	- It identifies the intrusions by monitoring and interpreting the communication on application-specific protocols.

+ Hybrid Intrusion Detection System :
`````````````````````````````````````
	- In the hybrid intrusion detection system, host agent or system data is combined with network information to develop a complete view of the network system.


Detection Method of IDS:
`````````````````````````
+ Signature-based:
``````````````````
- looking for specific patterns, such as byte sequences in network traffic
- Although signature-based IDS can easily detect known attacks
- it is impossible to detect new attacks, for which no pattern is available.

+ Anomaly-based:
````````````````
- a newer technology designed to detect and adapt to unknown attacks
- detection method uses machine learning to create a defined model of trustworthy activity, and then compare new behavior against this trust model.

-=-=-=-=-=-=


What is an Intrusion Prevention System?
```````````````````````````````````````

- An intrusion prevention system (IPS) is an network security device used to monitor and respond to potential threats.

- The main functions of an IPS are to identify suspicious activity, log relevant information, attempt to block the activity, and finally to report it.

Detection mechanisms:
`````````````````````

- Address matching
- HTTP string and substring matching
- Generic pattern matching
- TCP connection analysis
- Packet anomaly detection
- Traffic anomaly detection
- TCP/UDP port matching


IPS Classifications
```````````````````

Network-based intrusion prevention system (NIPS): 
`````````````````````````````````````````````````
- Analyzes protocol activity across the entire network, looking for any untrustworthy traffic.

Wireless intrusion prevention system (WIPS): 
````````````````````````````````````````````
- Analyzes network protocol activity across the entire wireless network, looking for any untrustworthy traffic.

Host-based intrusion prevention system (HIPS):
``````````````````````````````````````````````
- that follows a single host for malicious activity, and analyzes events occurring within said host.

IPS Detection Methods
`````````````````````
Signature-based detection: 
``````````````````````````
- Signature-based IDS monitors packets in the network and compares with predetermined attack patterns, known as “signatures”.

Statistical anomaly-based detection: 
````````````````````````````````````
- An anomaly-based IDS will monitor network traffic and compare it to expected traffic patterns. 

- The baseline will identify what is "normal" for that network – what sort of packets generally through the network and what protocols are used.

- it may raise a false positive alarms


Vulnerability/design/implementation:
````````````````````````````````````
SVG file network design.































======================================================
SNORT - Intrusion Prevention System (INLINE MODE)
	
Snort Modes
		1) Packet Capture Mode
				# snort -i eth0
		2) IDS Mode
		3) Inline Mode



1) Install SNORT:
``````````````````

CentOS:
````````
Manual:

# dnf install -y zlib-devel libpcap-devel pcre-devel libdnet-devel openssl-devel libnghttp2-devel luajit-devel gcc flex flex-devel bison

# wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz

# tar -xzvf daq-2.0.7.tar.gz
# cd daq-2.0.7
# ./configure && make && make install


# wget https://www.snort.org/downloads/snort/snort-2.9.20.tar.gz

# tar -xzvf snort-2.9.20.tar.gz

# cd snort-2.9.20/

# ./configure --enable-sourcefire --disable-open-appid [redhat]
# ./configure --enable-sourcefire && make && sudo make install [debian]

# make

# make install

Update lib:
````
# ldconfig
# ln -s /usr/local/bin/snort /usr/sbin/snort


Other stuff:
````````````
sudo groupadd snort
sudo useradd snort -r -s /sbin/nologin -c SNORT_IDS -g snort

sudo mkdir -p /etc/snort/rules
sudo mkdir /var/log/snort
sudo mkdir /usr/local/lib/snort_dynamicrules

sudo chmod -R 5775 /etc/snort
sudo chmod -R 5775 /var/log/snort
sudo chmod -R 5775 /usr/local/lib/snort_dynamicrules

sudo chown -R snort:snort /etc/snort
sudo chown -R snort:snort /var/log/snort
sudo chown -R snort:snort /usr/local/lib/snort_dynamicrules

sudo touch /etc/snort/rules/white_list.rules
sudo touch /etc/snort/rules/black_list.rules
sudo touch /etc/snort/rules/local.rules


sudo cp -av ~/snort-2.9.20/etc/*.conf* /etc/snort
sudo cp -av ~/snort-2.9.20/etc/*.map /etc/snort


wget https://www.snort.org/rules/community -O ~/community.tar.gz
tar -xvf ~/community.tar.gz -C ~/
cp ~/community-rules/* /etc/snort/rules


sed -i 's/include $RULE_PATH/#include $RULE_PATH/' /etc/snort/snort.conf
-------
# vim /etc/snort/snort.conf

change the default [~/root] path to [/etc/snort]

from:
`````
var RULE_PATH ../rules
var SO_RULE_PATH ../so_rules
var PREPROC_RULE_PATH ../preproc_rules
var WHITE_LIST_PATH ../rules
var BLACK_LIST_PATH ../rules

to:
```
var RULE_PATH /etc/snort/rules
var SO_RULE_PATH /etc/snort/so_rules
var PREPROC_RULE_PATH /etc/snort/preproc_rules
var WHITE_LIST_PATH /etc/snort/rules
var BLACK_LIST_PATH /etc/snort/rules







Debian/Ubuntu:
```````````````
$ sudo apt install snort -y

OR
$ sudo apt install -y gcc libpcre3-dev zlib1g-dev libluajit-5.1-dev 
libpcap-dev openssl libssl-dev libnghttp2-dev libdumbnet-dev 
bison flex libdnet autoconf libtool


Update shared libs: .so
```````````````````
# ldconfig
 
2. Info:
````````
# cat /etc/passwd | grep snort
OR
# id snort

snort:x:130:138:Snort IDS:/var/log/snort:/usr/sbin/nologin

3. Config:
```````````
# ls /etc/snort






























Rules
``````
# ls /etc/snort/rules

Log:
````
# ls /var/log/snort

main configuration file: /etc/snort/snort.conf

NOTE: take backup of original data.

# cp -av /etc/snort/snort.conf /etc/snort/snort.conf_orig_$(date -I)

4. Analyse config file:
```````````````````````
# vim /etc/snort/snort.conf

Comment this line:
#ipvar HOME_NET any

And add new line
ipvar HOME_NET 192.168.206.0/24

And comment all the rules except

local_rules.

:wq

Test the snort rule/config:
```````````````````````````
# snort -T -i enp0s3 -c /etc/snort/snort.conf

-T : Test
-i : interface
-c : config

Initializing rule chains...
0 Snort rules read
    0 detection rules
    0 decoder rules
    0 preprocessor rules
0 Option Chains linked into 0 Chain Headers







Time to configure own rules:
`````````````````````````````
** Snort rules are divided into two logical sections, the rule header and the rule options. **

1. Rule Header: The rule header contains the rule's `action, protocol, source and destination IP address and netmask, the source and destination port information`.

action
protocol
src ip
src port
dst ip
dst port











2. Rule Options: The rule option section contains alert message and information on which part of packet should be inspected to determine if rule action should be taken.


Rule Syntax:
````````````

<action> <proto> <src_ip> <src_port> -> <dst_ip> <dst_port> (msg:"<msg>"; sid:<signature>; rev:1;)



For custom rule, signature ID starts from 100001, before 100000 reserved for snort.


Rule Actions:
`````````````
alert		: Alert and log the packet
log		: log the packet
pass		: ignore the packet
drop		: block and log the packet
reject		: block the packet, log it and send TCP reset 
sdrop		: block the packet and do not log it




+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

________________________
a) ANY packet detection:
````````````````````````
# vim /etc/snort/rules/local.rules

alert ip any any -> any any (msg: "IP Packet detected"; sid: 100001; rev:1;) 

# snort -A console -q -i eth0 -c /etc/snort/snort.conf

02/13-12:39:48.921203  [**] [1:10000:1] IP Packet detected [**] [Priority: 0] {UDP} 143.244.134.227:123 -> 192.168.86.128:48971

















































______________________
b) PING Detection rule:
```````````````````````
# vim /etc/snort/rules/local.rules

alert icmp any any -> $HOME_NET any (msg: "LOL ICMP"; sid: 1000001; rev: 1;)

# snort -T -i eth0 -c /etc/snort/snort.conf	[ TEST ]
# snort -A console -q -i eth0 -c /etc/snort/snort.conf [ Debug ]

02/13-12:27:06.070450  [**] [1:1000001:1] LOL ICMP [**] [Priority: 0] {ICMP} 192.168.86.1 -> 192.168.86.128
02/13-12:27:06.070470  [**] [1:1000001:1] LOL ICMP [**] [Priority: 0] {ICMP} 192.168.86.128 -> 192.168.86.1

































































________________________________
c) FTP Connection Detection rule:
`````````````````````````````````

# vim /etc/snort/rules/local.rules

alert tcp any any -> $HOME_NET 21 (msg: "FTP Connection"; sid: 1000002; rev: 1;)

# snort -A console -q -i eth0 -c /etc/snort/snort.conf

02/13-12:32:43.635836  [**] [1:1000002:1] FTP Connection [**] [Priority: 0] {TCP} 192.168.86.1:37519 -> 192.168.86.128:21
02/13-12:32:43.636304  [**] [1:1000002:1] FTP Connection [**] [Priority: 0] {TCP} 192.168.86.1:37519 -> 192.168.86.128:21
02/13-12:32:43.692072  [**] [1:1000002:1] FTP Connection [**] [Priority: 0] {TCP} 192.168.86.1:37519 -> 192.168.86.128:21
02/13-12:32:45.712857  [**] [1:1000002:1] FTP Connection [**] [Priority: 0] {TCP} 192.168.86.1:37519 -> 192.168.86.128:21
02/13-12:32:45.714615  [**] [1:1000002:1] FTP Connection [**] [Priority: 0] {TCP} 192.168.86.1:37519 -> 192.168.86.128:21

______________________
d) FLAG detection rule:
```````````````````````
F - FIN 
S - SYN
R - RST
P - PSH
A - ACK
U - URG
0 (zero) - NO FLAG

There are also logical operators:
`````````````````````````````````
+ - ALL flag, match on all specified flags plus any others
* - ANY flag, match on any of the specified flags
! - NOT flag, match if the specified flags aren't set in the packet

# vim /etc/snort/rules/local.rules

alert tcp any any -> $HOME_NET any (flags: S; msg: "SYN Packet"; sid: 1000003; rev: 1;)


# snort -A console -q -i eth0 -c /etc/snort/snort.conf


NOTE: To check use 'scapy' IP()/TCP()

>>> a = IP()
>>> b = TCP()
>>> a.src = "x.x.x.x"
>>> a.dst = "x.x.x.x"
>>> b.flags = "S"
>>> send(a/b)

_________________________
e) Content Matching rule:
`````````````````````````
# vim /etc/snort/rules/local.rules

alert tcp any any -> $HOME_NET 22 (msg: "SSH Attempt"; content: "SSH"; sid: 1000003; rev: 1;)

# snort -A console -q -i eth0 -c /etc/snort/snort.conf

02/13-12:56:02.128231  [**] [1:1000003:1] SSH Attempt [**] [Priority: 0] {TCP} 192.168.86.1:38256 -> 192.168.86.128:22


NOTE: To check use 'scapy' IP()/TCP()

>>> a = IP()
>>> b = TCP()
>>> a.src = "x.x.x.x"
>>> a.dst = "x.x.x.x"
>>> b.flags = "S"
>>> send(a/b/"SSH")

