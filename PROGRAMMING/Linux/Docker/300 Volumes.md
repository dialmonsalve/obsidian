
### Anonymous volumen
Docker asigna el nombre único y el mismo lo utilize
```shell
docker run -v /var/lib/mysql/data
```

### Named volumen
El usuario asigna el nombre

#### Crear
```shell
docker volume create todo-db
```

#### Listar
```shell
docker volume ls
```

#### Inspeccionar
```shell
docker volume inspect todo-db
```

#### Remover uno
```shell
docker volume rm VOLUME_NAME
```

#### Remover todos
```shell
docker volume prune
```

#### Usar un volumen al correr contenedor
```shell
docker run -v todo-db:/etc/todos getting-started
```

### Bind volumes
Cuando se requiera hacer una conexión o vincular un file system con algún file system del contenedor. Sirve para hacer una imagen de so y conectar otras imagines
```shell
docker container run \
-w /app \
-p 80:3000 \
-v "$(pwd)":/app \
node:16-alpine3.16 \
sh -c "yarn install && yarn start:dev"
```