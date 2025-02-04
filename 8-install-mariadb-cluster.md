## INSTALLING MARIADB GALERA CLUSTER

### ON ALL CLUSTER NODES
```
yum install MariaDB-server
yum install MariaDB-client (already installed as part of MariaDB-server)
yum install galera-4 (already installed as part of MariaDB-server)

rpm -qa | grep -i mariadb && rpm -qa | grep -i galera

rpm -ql galera-4-26.4.20-1.el9.x86_64
Note down the path of Galera Replication Plugin Library i.e: /usr/lib64/galera-4/libgalera_smm.so
```
