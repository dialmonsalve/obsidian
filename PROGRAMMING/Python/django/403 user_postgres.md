
On the PostgreSQL terminal
```shell
Server <server>:
Database <postgres>:
Port <port>:
Username <postgres>:
Password to <user>: user:
psql (<version>)

postgres=# CREATE DATABASE dbempleado;
CREATE DATABASE
postgres=# CREATE USER dialm;
CREATE ROLE
postgres=# \c dbempleado;
#Ahora está conectado a la base de datos «dbempleado» con el usuario «postgres».
dbempleado=# ALTER ROLE dialm WITH PASSWORD '<password>';
ALTER ROLE
dbempleado=#
```

