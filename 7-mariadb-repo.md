## SETTING UP MARIADB REPOSITORY

### ON ALL CLUSTER NODES
```
vi /etc/yum.repos.d/MariaDB.repo

[mariadb]
name = MariaDB
baseurl = https://mirrors.accretive-networks.net/mariadb/yum/10.11/rhel/$releasever/$basearch
gpgkey = https://mirrors.accretive-networks.net/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck = 1


yum repolist
yum search MariaDB-server
yum info MariaDB-server
```
