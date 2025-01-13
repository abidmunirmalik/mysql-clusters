## CONFIRM VMs ARE READY 

### SSH & PING HOSTS
```
ping -c 3 gcn2
ping -c 3 gcn3

sestatus
rpm -qa | grep -i wsrep && rpm -qa | grep -i galera
```
