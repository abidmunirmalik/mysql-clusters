## MYSQL SHELL


### INSTALL MYSQL SHELL
```
https://dev.mysql.com/downloads/shell/
```


### STARTING MYSQL SHELL
```
mysqlsh

mysqlsh \sql - switch to SQL mode
mysqlsh \py - switch to Python Processing mode
mysqlsh \js - switch to JavaScript Processing mode
```


### GETTING HELP
```
mysqlsh
> \help \connect

SYNTAX:
\connect [<TYPE>] <URI>

URI: [user[:password]@]hostname[:port]
```

### CONNECTING VIA SQL MODE
```
EXAMPLE WITH LOGIN PATH CONFIGURED:
mysql_config_editor set --user=dba --password

mysqlsh dba@52.55.98.222 --sql

EXAMPLE WITHOUT LOGIN PATH CONFIGURED
mysql_config_editor remove --login-path=client

mysqlsh
mysqlsh> \connect --mysql dba@52.55.98.222:3306

VERIFY:
SELECT USER, SUM(CURRENT_CONNECTIONS), TOTAL_CONNECTIONS FROM performance_schema.accounts GROUP BY USER,CURRENT_CONNECTIONS, TOTAL_CONNECTIONS;
```

### CONNECTING VIA JAVASCRIPT SESSION
```
mysqlsh
mysqlsh>\js
shell.connect( {user:'dba', host:'52.55.98.222', port:3306} )

shell.status();
```


### CONNECTING VIA PYTHON SESSION
```
mysqlsh
mysqlsh>\py
> s = shell.open_session('mysql://dba@52.55.98.222:3306','P@ssw0rd123');
> s
```


