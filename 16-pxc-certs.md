## CONFIGURING PERCONA XTRADB CLUSTER SSL ECNRYPTION

### STOP MYSQL ON 2nd NODE
```
systemctl stop mysqld.service
```

### GET SSH PRIVATE KEY FROM LOCAL CLIENT
```
cat ~/.ssh/galera-cluster.pem
```

### CREATE PRIVATE KEY ON NODE1
```
vi ~/.ssh/cluster.pem
chmod 600 ~/.ssh/cluster.pem
```

### COPY CERTIFICATE FILES TO ALL OTHER NODES
```
scp -i ~/.ssh/galera-cluster.pem /var/lib/mysql/server-key.pem ec2-user@pxc2:/tmp/server-key.pem
scp -i ~/.ssh/galera-cluster.pem /var/lib/mysql/ca.pem ec2-user@pxc2:/tmp/ca.pem
scp -i ~/.ssh/galera-cluster.pem /var/lib/mysql/server-cert.pem ec2-user@pxc2:/tmp/server-cert.pem

scp -i ~/.ssh/galera-cluster.pem /var/lib/mysql/server-key.pem ec2-user@pxc3:/tmp/server-key.pem
scp -i ~/.ssh/galera-cluster.pem /var/lib/mysql/ca.pem ec2-user@pxc3:/tmp/ca.pem
scp -i ~/.ssh/galera-cluster.pem /var/lib/mysql/server-cert.pem ec2-user@pxc3:/tmp/server-cert.pem
```

### REPLACE CERTIFICATE FILES ON NODE 2 & 3
```
ls -ltr /var/lib/mysql/ca.pem
ls -ltr /var/lib/mysql/server-key.pem
ls -ltr /var/lib/mysql/server-cert.pem

mv /tmp/ca.pem /var/lib/mysql/ca.pem
mv /tmp/server-key.pem /var/lib/mysql/server-key.pem
mv /tmp/server-cert.pem /var/lib/mysql/server-cert.pem

ls -ltr /var/lib/mysql/ca.pem

chown mysql:mysql /var/lib/mysql/ca.pem
chown mysql:mysql /var/lib/mysql/server-key.pem
chown mysql:mysql /var/lib/mysql/server-cert.pem

ls -ltr /var/lib/mysql/ca.pem
```

### START PXC SERVER ON NODE 2 & 3
```
systemctl start mysqld.service
```
