## REMOVING MARIADB GALERA CLUSTER

### STOP MYSQL ON ALL CLUSTER NODES
```
systemctl stop mariadb.service
```

### RUN ON ALL THE NODES
```
rpm -qa | grep -i mariadb

yum -y remove MariaDB-server-10.11.10-1.el9.x86_64

rpm -qa | grep -i galera 

grep mysql /etc/passwd

userdel -r mysql

rm -f /var/log/mariadb.log

rm -f /etc/my.cnf && rm -rf /etc/my.cnf.d
```

### REBOOT HOST
```
reboot | init 6
```
