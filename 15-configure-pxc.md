## CONFIGURING PERCONA XTRADB CLUSTER

### STOP MYSQL ON ALL CLUSTER NODES
```
systemctl stop mysqld.service
```

### CREATE CLUSTER CONFIG FILE ON ALL CLUSTER NODES
```
vi /etc/my.cnf.d/cluster.cnf

[mysqld]
wsrep_provider           = /usr/lib64/galera4/libgalera_smm.so
wsrep_cluster_address    = gcomm://pxc1,pxc2,pxc3
binlog_format            = ROW
wsrep_slave_threads      = 8
innodb_autoinc_lock_mode = 2
wsrep_node_address       = 172.31.82.218
wsrep_cluster_name       = pxc-cluster
wsrep_node_name          = pxc1
pxc_strict_mode          = ENFORCING
wsrep_sst_method         = xtrabackup-v2
wsrep_log_conflicts
```

### CREATE CLUSTER SSL ENCRYPTION FILE ON ALL CLUSTER NODES
```
vi /etc/my.cnf.d/ssl.cnf

[mysqld]
wsrep_provider_options="socket.ssl_key=server-key.pem;socket.ssl_cert=server-cert.pem;socket.ssl_ca=ca.pem"

[sst]
encrypt  = 4
ssl-key  = server-key.pem
ssl-ca   = ca.pem
ssl-cert = server-cert.pem
```


### BOOTSTRAP PXC CLUSTER - ONLY ON NODE 1
```
systemctl start mysql@bootstrap.service
```


### VERIFY PXC CLUSTER
```
mysql
> show status like 'wsrep_cluster%';
> create database finance;
```
