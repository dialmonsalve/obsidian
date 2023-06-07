
### Mariadb
```shell
docker container run \
-dp 3306:3306 \
--name world-db \
-e MARIADB_USER=example-user \
-e MARIADB_PASSWORD=user-password \
-e MARIADB_ROOT_PASSWORD=root-secret-password \
-e MARIA_DATABASE=world-db \
--volume world-db:/var/lib/mysql \
--network world-app \
mariadb:jammy
```

### phpmyadmin
```shell
docker container run \
--name phpmyadmin \
-dp 8080:80 \
-e PMA_ARBITRARY=1 \
--network world-app \
phpmyadmin:5.2.0-apache 
```

#### pgAdmin
```shell
docker container run \
-e PGADMIN_DEFAULT_PASSWORD=123456 \
-e PGADMIN_DEFAULT_EMAIL=superman@google.com \
-dp 8080:80 \
dpage/pgadmin4:6.17
```

#### postgres
```shell
docker container run \
-d \
--name postgres-db \
-e POSTGRES_PASSWORD=123456 \
-v postgres-db:/var/lib/postgresql/data \
postgres:15.1
```

