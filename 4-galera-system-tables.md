## GALERA CLUSTER SYSTEM TABLES


### CURRENT STATUS OF GALERA CLUSTER
```
> SHOW STATUS LIKE 'wsrep%';
```


### GALERA SYSTEM TABLES 

* Galera version 4 - New replication related system tables:
```
> SHOW TABLES FROM mysql LIKE 'wsrep%';
wsrep_cluster
wsrep_cluster_members
wsrep_streaming_log
```



### WSREP_CLUSTER System Table
* Provides current view of the installed Galera cluster:
```
> SELECT * FROM mysql.wsrep_cluster;
```
* **cluster_uuid** - The unique cluster UUID, check `wsrep_local_state_uuid` status.
* **view_id** - The number of config changes in the Galera cluster, check `wsrep_cluster_conf_id` status.
* **view_seqno** - The unique identifier associated with each transaction, check `wsrep_last_committed` status.
* **protocol_version** - It's the protocol version of the MySQL-wsrep.
* **capabilities** - It's the metadata needed to recover node state during crash recovery



### WSREP_CLUSTER_MEMBERS System Table
* This system table provides each cluster node information:
```
select * from mysql.wsrep_cluster_members;
```
* **node_uuid** - The unique UUID, the identifier of each node.
* **node_name** - What we have defined in the `galera-cluster.cnf` file using `wsrep-node-name`.
* **node_incoming_address** - stores the IP address and port on which each node is listening for client connections.


### WSREP_STREAMING_LOG System Table
* New feature introduced in Galera cluster 4.
* Used for **Streaming Replication** - Only active if you **enable** the ongoing streaming transactions.
* Under normal operation, the node performs all replication and certification events when a transaction commits.
* Used for large transactions where node breaks the transaction into fragments, then certifies and replicates them on the replicas while the transaction is still in progress
* Streaming Replication allows the node to process transaction write-sets greater than 2Gb.
