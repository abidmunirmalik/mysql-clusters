## CONFIGURING MARIADB GALERA CLUSTER

### STOP MYSQL ON ALL CLUSTER NODES
```
systemctl stop mariadb.service
```

### CREATE CLUSTER CONFIG FILE ON ALL CLUSTER NODES
```
vi /etc/my.cnf.d/cluster.cnf

[mysqld]
binlog_format            = ROW
innodb-autoinc-lock-mode = 2
bind-address             = 0.0.0.0

wsrep_on                 = ON
wsrep_provider           = "/usr/lib64/galera-4/libgalera_smm.so"
wsrep_cluster_name       = "mariadb-cluster"
wsrep_cluster_address    = "gcomm://mcn1,mcn2,mcn3"
wsrep_sst_method         = rsync
wsrep_node_address       = "172.31.82.27"
wsrep_node_name          = "mcn1"
```

### BOOTSTRAP CLUSTER - ONLY ON NODE 1
```
galera_new_cluster
```

### START MYSQL ON ALL OTHER CLUSTER NODES
```
systemctl start mariadb.service
```

### VERIFY MARIADB CLUSTER
```
mysql
show status like 'wsrep_cluster%';
```
