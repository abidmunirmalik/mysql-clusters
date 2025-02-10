## REMOVING MEMBER FROM XTRADB CLUSTER

### REMOVING MEMBER
- No  need to stop or reboot other cluster members
- Other cluster members will automatically pick the removal
- Reome the entry from other members's cluster config so on-reboot, they don't try to connect


### STOP MYSQL
```
systemctl stop mysqld.service
```

### REMOVE CLUSTER RELEATED FILES
```
rm -f /etc/my.cnf.d/cluster.cnf
rm -f /etc/my.cnf.d/ssl.cnf
```

### DELETE MEMBER ENTRY ON OTHER MEMBERS
```
vi /etc/my.cnf.d/cluster.cnf
#wsrep_cluster_address    = gcomm://pxc1,pxc2,pxc3
#wsrep_cluster_address    = gcomm://pxc1,pxc2
```

