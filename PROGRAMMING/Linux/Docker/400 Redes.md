
Conexión entre contenedores:
```shell
docker network

#Comandos:
connect
create
disconnect
inspect
ls
prune
rm
```

#### Conectar contenedores
```shell
docker network connect $NOMBRE_RED $ID_CONTAINER

docker network connect $NOMBRE_RED $ID_OTRO_CONTAINER
```

#### Para ver los contenedores conectados a la red
```shell
docker network inspect $NOMBRE_RED
```