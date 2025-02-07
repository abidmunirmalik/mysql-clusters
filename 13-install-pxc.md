## INSTALLING PERCONA XTRADB CLUSTER

### ON ALL CLUSTER NODES
```
yum search percona-xtradb-cluster
yum info percona-xtradb-cluster
yum install percona-xtradb-cluster


rpm -qa | grep -i  percona
rpm -ql percona-xtradb-cluster-server-8.0.40-31.1.el9.x86_64

Note down the path of Galera Replication Plugin Library i.e: /usr/lib64/galera-4/libgalera_smm.so
```
