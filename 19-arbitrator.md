## CONFIGURING GALERA CLUSTER ARBITRATOR


### INSTALL ARBITRATOR ON PXC
```
yum search garbd
yum install percona-xtradb-cluster-garbd.x86_64

rpm -ql percona-xtradb-cluster-garbd-8.0.40-31.1.el9.x86_64
/etc/sysconfig/garb - Arbitrator configuration file
/usr/bin/garbd - Arbitrator Daemon process
/usr/lib/systemd/system/garb.service - Arbitrator Service
```


### START ARBITRATOR
```
garbd --group=pxc-cluster --address="gcomm://172.31.82.27:4567,172.31.86.128:4567" --options="socket.ssl=yes;socket.ssl_key=/var/lib/mysql/server-key.pem;socket.ssl_cert=/var/lib/mysql/server-cert.pem;socket.ssl_ca=/var/lib/mysql/ca.pem;socket.ssl_cipher=AES128-SHA256" --log=/var/log/arbitrator.log
```


### WATCH ARBITRATOR
```
ps aux | grep -i garb
> select * from mysql.wsrep_cluster_members;
> show status like 'wsrep_cluster%';

grep -A 5 -B 5 -i members /var/log/mysqld.log (Note Primary/Total should be 2/3)
```

