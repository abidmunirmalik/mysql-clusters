## GALERA CLUSTER SETUP

### GALERA 4 REPLICATION LIBRARY
**Download Site:** https://galeracluster.com/downloads/

**Version:** Galera 4 Replication Library, Version 26.4.21

**OS:** Red Hat Enterprise Linux 9
```
ssh -i ~/.ssh/galera root@164.92.80.80
sudo -i
mkdir -p /tmp/galera-cluster && cd /tmp/galera-cluster
yum install -y wget
wget https://releases.galeracluster.com/galera-4/redhat/9/x86_64/galera-4-26.4.21-1.el9.x86_64.rpm
yum localinstall -y galera-4-26.4.21-1.el9.x86_64.rpm
rpm -qa | grep galera
rpm -ql galera-4-26.4.21-1.el9.x86_64
```

### MYSQL SERVER WITH WSREP
**Download Site:** https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/
* Download the RPMs
```
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-8.0-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-client-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-client-plugins-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-common-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-devel-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-icu-data-files-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-libs-8.0.40-26.21.el9.x86_64.rpm
wget https://releases.galeracluster.com/mysql-wsrep-8.0/redhat/9/x86_64/mysql-wsrep-server-8.0.40-26.21.el9.x86_64.rpm
```

* Locally Install the RPMs
```
yum localinstall -y mysql-wsrep-client-plugins-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-common-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-libs-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-client-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-devel-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-icu-data-files-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-server-8.0.40-26.21.el9.x86_64.rpm
yum localinstall -y mysql-wsrep-8.0-8.0.40-26.21.el9.x86_64.rpm
```

* Verify the RPMs
```
rpm -qa | grep -i mysql-wsrep
```
