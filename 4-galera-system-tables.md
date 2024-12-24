## GALERA CLUSTER SYSTEM TABLES

### GALERA SYSTEM TABLES 

* Galera version 4 - New replication related system tables:
```
> show tables from mysql like 'wsrep%';
wsrep_cluster
wsrep_cluster_members
wsrep_streaming_log
```


### WSREP_CLUSTER SYSTEM TABLE
* Provides cluster information of the installed Galera cluster
