## GALERA CLUSTER SETUP

### GALERA 4 REPLICATION LIBRARY
Download Site: https://galeracluster.com/downloads/
Version: Galera 4 Replication Library, Version 26.4.21 
OS: Red Hat Enterprise Linux 9
```
mkdir -p /tmp/galera
cd /tmp/galera
wget https://releases.galeracluster.com/galera-4/redhat/9/x86_64/galera-4-26.4.21-1.el9.x86_64.rpm
yum localinstall galera-4-26.4.21-1.el9.x86_64.rpm
rpm -ql galera-4-26.4.21-1.el9.x86_64
```
