## REMOVING GALERA CLUSTER


### ON NODE 2
```
systemctl stop mysqld.service
rpm -qa | grep mysql-wsrep
yum remove -y mysql-wsrep-devel-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-client-plugins-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-icu-data-files-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-common-8.0.40-26.21.el9.x86_64

rpm -qa | grep galera
yum remove -y galera-4-26.4.21-1.el9.x86_64

userdel -r mysql
rm -rf /etc/my.cnf*
rm -f /var/log/mysqld.log
init 6
```

### ON NODE 1
```
systemctl stop mysqld.service
rpm -qa | grep mysql-wsrep
yum remove -y mysql-wsrep-devel-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-client-plugins-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-icu-data-files-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-common-8.0.40-26.21.el9.x86_64

rpm -qa | grep galera
yum remove -y galera-4-26.4.21-1.el9.x86_64

userdel -r mysql
rm -rf /etc/my.cnf*
rm -f /var/log/mysqld.log
init 6
```
