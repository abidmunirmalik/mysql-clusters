## STARTING & SECURING MARIADB SERVER

### ON ALL CLUSTER NODES
```
ls /etc/my*
less /etc/my.cnf

rm -f /etc/my.cnf.d/client.cnf 
rm -f /etc/my.cnf.d/mysql-clients.cnf
rm -f /etc/my.cnf.d/spider.cnf

vi /etc/my.cnf.d/server.cnf
[mysqld]
datadir   = /var/lib/mysql
socket    = /var/lib/mysql/mysql.sock
log-error = /var/log/mariadb.log
pid-file  = /var/lib/mysql/mariadb.pid


systemctl start mariadb.service
systemctl status mariadb.service


mariadb-secure-installation

mysql -u root -p
> \s
> exit

ls /var/lib/mysql
tail /var/log/mariadb.log 
pidof mariadbd
```
