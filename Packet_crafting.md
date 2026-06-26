# Packet crafting in python using Scapy framework

#### On Kali

1. Install Scapy

```sudo apt install python3-scapy -y```

2. Execute a command (it will opent the framework)

```sudo scapy```

i. Craft TCP and IP packets

```
# craft IP & TCP 
a= IP()
b= TCP()

# To check the raw header
a.show()

# Config IP packet
#Change the source and distination Ip
a.src = 'Attackers_Ip'
a.dst = 'target_Ip'

# Config TCP packet
#Change the flag
b.flags = "F"
b.show()

send(a/b, count=1) # a/b = for merge count = how much packet you want to send
send(a/b, count=1)
send(a/b, loop=1) # to send packet in loop
send(a/b/'data', loop=1) # To increase the packet size (in data that i write here you can write anything eg:- 'ajhfayafafiabcdahfa')
```
