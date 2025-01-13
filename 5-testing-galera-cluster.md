## TESTING GALERA CLUSTER


### CURRENT STATUS OF GALERA CLUSTER
```
> SHOW STATUS LIKE 'wsrep%';
```
* Pay close attention to these variables:
  * wsrep_local_state_comment
  * wsrep_cluster_size
  * wsrep_ready
 
### SIMULATE THE FAILURE
* On any of the node, shutdown `mysqld.service`:
```
systemctl stop mysqld.service
```
* On one of the remaining nodes:
```
> INSERT INTO finance.employees values();
> select * from finance.employees; from another node
```
* Open two tabs on the shutdown node
* On one tab run `systemctl start mysqld.service`
* On the other tab observe the `tail -f /var/log/mysqld.log`
* Search for `Processing event queue`, `Shifting`
