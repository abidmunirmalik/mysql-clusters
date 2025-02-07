## SETTING UP PERCONA REPOSITORY

### ON ALL CLUSTER NODES
```
yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

percona-release show
percona-release setup pxc-80
percona-release show
```
