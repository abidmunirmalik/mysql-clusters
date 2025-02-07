## STARTING & SECURING PERCONA XTRADB CLUSTER SERVER

### ON ALL CLUSTER NODES
```
ls /etc/my*
less /etc/my.cnf

cp /etc/my.cnf /etc/my.cnf.original

/etc/my.cnf
!includedir /etc/my.cnf.d


vi /etc/my.cnf.d/server.cnf
[mysqld]
server-id                  = 1
datadir                    = /var/lib/mysql
socket                     = /var/lib/mysql/mysql.sock
log-error                  = /var/log/mysqld.log
pid-file                   = /var/run/mysqld/mysqld.pid
binlog_expire_logs_seconds = 604800
```

### START PXC SERVER
```
systemctl start mysqld.service
systemctl status mysqld.service
```

### SECURE PXC SERVER
```
grep temporary /var/log/mysqld.log

mysql_secure_installation
Note: If you get following error
`Error: Access denied for user 'root'@'localhost' (using password: YES)`

mysql_config_editor print
mysql_config_editor remove --login-path=client

mysql_secure_installation

mysql_config_editor set --user=root --password
```
