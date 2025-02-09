## SETTING UP PERCONA REPOSITORY

### CLEANUP REPOS - ON ALL CLUSTER NODES
```
rm -f /etc/yum.repos.d/MariaDB.repo
yum clean all
```

### SETUP PERCONA REPO - ON ALL CLUSTER NODES
```
yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

ls /etc/yum.repos.d/

percona-release show
perona-release --help

percona-release setup pxc-80
percona-release show

yum search percona-xtradb-cluster
```
