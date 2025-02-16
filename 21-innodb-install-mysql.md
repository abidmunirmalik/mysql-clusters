## SETUP INNODB CLUSTER


### INSTALL MYSQL SERVER PACKAGE - ALL 3 NODES
```
yum install  https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm

yum search mysql
yum info mysql-community-server.x86_64

yum install mysql-community-server.x86_64
```


### CONFIGURE MYSQL
```
(
mkdir -p /var/log/mysql/relaylog
mkdir -p /var/log/mysql/binlog
chown -R mysql:mysql /var/log/mysql
)

vi /etc/my.cnf

[mysqld]
datadir         =  /var/lib/mysql
socket          =  /var/lib/mysql/mysql.sock
log-error       =  /var/log/mysqld.log
pid-file        =  /var/run/mysqld/mysqld.pid
log-bin         =  /var/log/mysql/binlog/mysqld-bin
log-bin-index   =  /var/log/mysql/binlog/mysqld-bin.index
relay-log       =  /var/log/mysql/relaylog/mysqld-relay-bin
relay-log-index =  /var/log/mysql/relaylog/mysqld-relay-bin.index
```

### START MYSQL ON REPLICA
```
systemctl start mysqld.service
```

### SECRURE INSTALLATION
```
grep temporary /var/log/mysqld.log

mysql_secure_installation

mysql_config_editor set --user=root --password

> \s

> CREATE USER dba IDENTIFIED BY 'P@ssw0rd123';

> GRANT ALL PRIVILEGES ON *.* TO dba WITH GRANT OPTION;
```
