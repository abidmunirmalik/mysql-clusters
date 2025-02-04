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

### CREATE EC2 
```
Name     : gcn1
OS       : Red Hat Enterprise Linux 9
AMI      : ami-0c7af5fe939f2677f
Arch     : 64-bit (x86)
Region   : N. Virginia
Instance : t2.micro
Key Pair : galera-cluster
Public IP: Enable
Sec Group: galera-cluster-sg
Storage  : 10 GB (gp3)
```

### CONNECT TO EC2
```
ssh -i ~/.ssh/galera-cluster.pem ec2-user@<pubic_ip_gcn1>
sudo hostnamectl hostname gcn1 && sudo hostnamectl status
ip address

vi /etc/hosts
# Galera Cluster Setup
172.31.21.160 gcn1.gcluster.local gcn1
```

### CREATE TWO MORE RHEL VMs
```
Name    : gcn2 & gcn3
ssh -i ~/.ssh/galera-cluster.pem ec2-user@<pubic_ip_gcnx>
sudo hostnamectl hostname gcn2 && sudo hostnamectl status

cat /etc/hosts
# Galera Cluster Setup
172.31.21.160 gcn1.gcluster.local gcn1
172.31.26.227 gcn2.gcluster.local gcn2
172.31.22.24  gcn3.gcluster.local gcn3

ping -c 3 gcn3.gclluster.local && ping -c 3 gcn2
```

### DISABLE SELINUX & REBOOT
```
vi /etc/selinux/config
  SELINUX=disabled
grubby --update-kernel ALL --args selinux=0
init 6
```
