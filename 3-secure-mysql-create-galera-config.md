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

* Fetch temporary password and run secure installation
```
grep -i "temporary password" /var/log/mysqld.log
mysql_secure_installation
mysql -u root -p
mysql_config_editor set --user=root --password
mysql_config_editor print
mysql
```
