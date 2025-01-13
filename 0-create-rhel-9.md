## RED HAT ENTERPRISE LINUX SETUP

### CREATE SSH KEY PAIR
```
Name         : galera-cluster
Key pair type: ED25519
Key format   : .pem

mv ~/Downloads/galera-cluster.pem ~/.ssh/
cd ~/.ssh && chmod 600 galera-cluster.pem && ls -ltr galera-cluster.pem
```

### CREATE SECURITY GROUP
```
Name         : galera-cluster-sg
Inbound rules:
     Type    : SSH
     Port    : 22
     Source  : 0.0.0.0/0
     Tag     : SSH Access

     Type    : MySQL/Aurora
     Port    : 3306
     Source  : 0.0.0.0/0
     Tag     : MySQL Access

     Type    : Custom TCP
     Port    : 4444
     Source  : galera-cluster-sg
     Tag     : State Snapshot Transfer SST Traffic

     Protocol: Custom TCP
     Port    : 4567
     Source  : galera-cluster-sg
     Tag     : Replication Traffic

     Protocol: Custom TCP
     Port    : 4568
     Source  : galera-cluster-sg
     Tag     : Incremental State Transfer IST Traffic

     Protocol: All ICMP - IPv4
     Port    : All
     Source  : galera-cluster-sg
     Tag     : ping
```
