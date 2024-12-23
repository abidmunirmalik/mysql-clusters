## GALERA CLUSTER PREPARE

### PREPARE HOSTS FOR GALERA CLUSTER

* Disable SELINUX
```
vi /etc/selinux/config
  SELINUX=disabled
grubby --update-kernel ALL --args selinux=0
init 6
```

* Edit /etc/hosts file
```
# Galera Cluster Setup
10.124.0.2 g1.gcluster.local g1
10.124.0.4 g2.gcluster.local g2
10.124.0.3 g3.gcluster.local g3
```

* Verify ping hosts
```
ping g2.gcluster.local
ping g3
```
