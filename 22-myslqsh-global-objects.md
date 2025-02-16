## MYSQL SHELL GLOBAL OBJECTS


**MySQL Shell includes many global objects available in javaScript & Python processing modes**
* session - Available when session is established i.e connected to MySQL server
* dba - Provides access to InnoDB cluster
* cluster - Represent InnoDB cluster
* rs - Represent a InnoDB Replica Set
* db - 
* shell
* util


### SHELL GLOBAL OBJECT
```
mysqlsh dba@52.55.98.222 --sql
>\js
>session.help()

>session.isOpen()
true

>session.getUri()
mysql://dba@52.55.98.222:3306


>var allUsers = session.runSql("SELECT user,host FROM mysql.user order by 1");
>allUsers

>var row = allUsers.fetchOneObject();
>print(row['user'],row['host']);
```
