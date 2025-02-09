## PERCONA XTRADB CLUSTER SST METHOD

### STATE SNAPSHOT TRANSFER METHODS IN PXC CLUSTER
1. mysqldump
2. rsync
3. xtrabackup

**Note:** 
  - The `mysqldump` and `rsync` will cause the **DONER NODE** to become **READ-ONLY** while data is being copied.
  - The `xtrabackup` uses **backup locks** which means the Galera Provider is not paused at all as with `FLUSH TABLE WITH READ LOCK`.
  - The default SST method is `xtrabackup-v2` which uses Percona XtraBackup.
 

### OBSERVE THE MYSQLD.LOG FILE ON ALL CLUSTER NODES
```
grep rsync /var/log/mysqld.log (no ouput should be expected)
grep WSREP-SST /var/log/mysqld.log
grep xtrabackup /etc/my.cnf.d/cluster.cnf
show global variables  like '%sst%';
```
