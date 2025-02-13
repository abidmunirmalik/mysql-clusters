## SETUP PXC REPLICA


### REMOVE EXISTING PXC PACKAGES
```
systemctl stop mysqld.service

rpm -qa | grep percona
yum remove -y percona-xtradb-cluster-server-8.0.40-31.1.el9.x86_64
yum remove -y percona-xtradb-cluster-garbd-8.0.40-31.1.el9.x86_64
yum remove -y percona-release-1.0-29.noarch

userdel -r mysql
rm -rf /etc/my*

rm -f /var/log/mysqld.log
rm -f /var/log/arbitrator.log

yum clean all
yum repolist

init 6
```


### INSTALL MYSQL SERVER
```
yum install  https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm

yum search mysql
yum info mysql-community-server.x86_64

yum install mysql-community-server.x86_64
```


### START MYSQL
```
mkdir -p /var/log/mysql/relaylog
mkdir -p /var/log/mysql/binlog
chown -R mysql:mysql /var/log/mysql

vi /etc/my.cnf

[mysqld]
server-id       =  5
datadir         =  /var/lib/mysql
socket          =  /var/lib/mysql/mysql.sock
log-error       =  /var/log/mysqld.log
pid-file        =  /var/run/mysqld/mysqld.pid
# Replica Setup
log-bin         =  /var/log/mysql/binlog/mysqld-bin
log-bin-index   =  /var/log/mysql/binlog/mysqld-bin.index
relay-log       =  /var/log/mysql/relaylog/mysqld-relay-bin
relay-log-index =  /var/log/mysql/relaylog/mysqld-relay-bin.index
# Replica Options
skip_replica_start

systemctl start mysqld
```

### INSTALL XTRABACKUP ON PXC MEMBER
```
yum install percona-xtrabackup-80.x86_64
```

### CONFIGURE LOG SLAVE UPDATES ON PXC MEMBER
```
show global variables like 'log_slave%';
```

### CREATE REPLICATION ADMIN USER ON PXC MEMBER
```
CREATE USER replicator IDENTIFIED BY 'P@ssw0rd123';
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO bob;
```

### PERFORM ONLINE BACKUP WITH XTRABACKUP
```
mkdir /tmp/full_backup
mkdir /tmp/restore (on replica host)
xtrabackup --backup --open-files-limit=256000  --target-dir=/tmp/full_backup/
xtrabackup --prepare  --target-dir=/tmp/full_backup
```

### SCP ONLINE BACKUP FROM PXC TO REPLICA
```
chown -R ec2-user:ec2-user /tmp/full_backup
scp -i ~/.ssh/cluster.pem -r full_backup/* ec2-user@pxc3:/tmp/restore/
```

### RESTORE XTRABACKUP
```
chown -R ec2-user:ec2-user /tmp/restore/

systemctl stop mysqld.service
cp -r /tmp/restore/* /var/lib/mysql/
chown -R mysql:mysql /var/lib/mysql
```

### START MYSQL ON REPLICA
```
systemctl start mysqld.service
```

### CONFIGURE REPLICA
```
less /var/lib/mysql/xtrabackup_binlog_info

CHANGE REPLICATION SOURCE TO SOURCE_HOST='pxc1', SOURCE_USER='replicator', SOURCE_PASSWORD='P@ssw0rd123', SOURCE_LOG_FILE='', SOURCE_LOG_POS=;

start replica;

show replica status\G
```

