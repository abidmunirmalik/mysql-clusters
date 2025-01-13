## REMOVING GALERA CLUSTER


### ON ALL CLUSTER NODES
```
systemctl stop mysqld.service
rpm -qa | grep mysql-wsrep
yum remove -y mysql-wsrep-devel-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-client-plugins-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-icu-data-files-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-common-8.0.40-26.21.el9.x86_64

rpm -qa | grep galera
yum remove -y galera-4-26.4.21-1.el9.x86_64

rpm -qa | grep -i galera && rpm -qa | grep -i mysql

cat /etc/passwd | grep -i mysql
ls -ltr /var/lib/mysql

userdel -r mysql

ls /etc/my*

rm -rf /etc/my*

ls /var/log/mysqld.log
rm -f /var/log/mysqld.log
init 0
```
