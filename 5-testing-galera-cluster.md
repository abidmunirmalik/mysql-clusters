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
> INSERT INTO finance.employees(first_name) VALUES('John Doe');
> select * from finance.employees; from another node
```
* Open two tabs on the shutdown node
* On one tab run `systemctl start mysqld.service`
* On the other tab observe the `tail -f /var/log/mysqld.log`


### REMOVING NODE FROM GALERA CLUSTER
1. Stop the `mysqld.service`:
```
systemctl stop mysqld.service
```
3. Remove the reference of the node from `wsrep_cluster_address` in the `galera_cluster.cnf` file:
```
# wsrep_cluster_address  = "gcomm://g1.gcluster.local,g2.gcluster.local,g3.gcluster.local"
wsrep_cluster_address  = "gcomm://g1.gcluster.local,g2.gcluster.local"
```
4. No need to re-start other node members
```
select * from mysql.wsrep_cluster_members;
```
6. Uninstall the Galera cluster software
```
rpm -qa | grep mysql-wsrep
yum remove -y mysql-wsrep-devel-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-client-plugins-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-icu-data-files-8.0.40-26.21.el9.x86_64
yum remove -y mysql-wsrep-common-8.0.40-26.21.el9.x86_64

rpm -qa | grep -i galera
yum remove -y galera-4-26.4.21-1.el9.x86_64

userdel -r mysql
rm -rf /etc/my.cnf.d/
rm -f /etc/my.cnf*
rm -f /var/log/mysqld.log
ls /usr/bin/mysql*
```
 

### SPLIT-BRAIN SIMULATION
* The Split-Brain simulation can be performed on two-node cluster
* shutdown 
