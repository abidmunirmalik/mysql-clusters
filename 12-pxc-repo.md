## SETTING UP PERCONA REPOSITORY

### ON ALL CLUSTER NODES
```
yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

percona-release show
perona-release --help

percona-release setup pxc-80
percona-release show

yum search percona-xtradb-cluster
```
