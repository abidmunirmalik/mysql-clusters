## MYSQL SECURE INSTALLATION & GALERA CONFIGURATION

### START & SECURE MYSQL 

* Edit the my.cnf file
```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock

log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
```

* Start mysqld service
```
systemctl start mysqld.service
pidof mysqld
```

* Fetch temporary password and run secure installation - All members
```
grep -i "temporary password" /var/log/mysqld.log
mysql_secure_installation
mysql -u root -p
mysql_config_editor set --user=root --password
mysql_config_editor print
mysql
```

### CONFIGURATION FOR GALERA CLUSTER
* Perform the following tasks on each member of the cluster
```
systemctl stop mysqld.service

vi /etc/my.cnf
 !includedir /etc/mysql/conf.d/

touch /etc/mysql/conf.d/mysql-server.cnf && touch /etc/mysql/conf.d/galera-cluster.cnf

vi /etc/mysql/conf.d/mysql-server.cnf
 [mysqld]
 datadir=/var/lib/mysql
 socket=/var/lib/mysql/mysql.sock
 user=mysql
 log-error=/var/log/mysqld.log
 pid-file=/var/run/mysqld/mysqld.pid

vi /etc/mysql/conf.d/galera-cluster.cnf
 [mysqld]
 # MySQL-WSREP Configuration
 binlog_format             = ROW
 default-storage-engine    = innodb
 innodb-autoinc-lock-mode  = 2
 bind-address              = 0.0.0.0

 # Write Set Replication Plugin Configuration
 wsrep_on                  = ON
 wsrep_provider            = /usr/lib64/galera-4/libgalera_smm.so
 wsrep_cluster_name        = "gcluster"
 wsrep_cluster_address     = "gcomm://"
 #wsrep_cluster_address     = "gcomm://g1.gcluster.local,g2.gcluster.local,g3.gcluster.local"
 wsrep_sst_method          = rsync
 wsrep_node_address        = "172.31.46.28"
 wsrep_node_name           = "g1.gcluster.local"
```

* Attempt to Bootstrap first member of the cluster
```
systemctl start mysqld@bootstrap.service
systemctl status mysqld.service
```

* Start MySQL service on 2nd & 3rd members of the cluster
```
systemctl start mysqld.service
mysql
> show status like 'wsrep_cluster%';
> show tables from mysql like 'wsrep_%';
> select * from mysql.wsrep_cluster;
> select * from mysql.wsrep_cluster_members;
> select * from mysql.wsrep_streaming_log;
```

* Test the Write-Set Replication from first member
```
mysql
> CREATE DATABASE finance;
> USE finance;
> CREATE TABLE employees(ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT);
> exit;
```

* On first member stop the Bootstrap Service and re-start MySQL Service
```
systemctl stop mysqld@bootstrap.service
vi /etc/mysql/conf.d/galera-cluster.cnf
 wsrep_cluster_address     = "gcomm://g1.gcluster.local,g2.gcluster.local,g3.gcluster.local"
systemctl start mysqld.service
```
