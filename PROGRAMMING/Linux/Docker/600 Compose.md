
## docker-compose.yaml

### Postgres
#### Named volumen
```yml
version:'3'

services:
	# Nombre del servicio
	db:
		container_name: postgres_database
		image: postgres:15.1
		volumes:
			- postgres-db:/var/lib/postgresql/data
		environment:
			- POSTGRES_PASSWORD=123456
			
	pgAdmin:
		depends_on:
			- db
		image: dpage/pgadmin4:6.17
		ports:
			- "8080:80"
		environment:
			- PGADMIN_DEFAULT_PASSWORD=123456
			- PGADMIN_DEFAULT_EMAIL=superman@google.com

# Crea las imagenes con un volumen especifico. Si no se pasa, docker lo crea de manera automática
volumes:
	postgres-db:
		external: true
```

#### Bind volumes
```yaml
version:'3'

services:
	# Nombre del servicio
	db:
		container_name: postgres_database
		image: postgres:15.1
		volumes:
			- ./postgres:/var/lib/postgresql/data # Relativo al path
		environment:
			- POSTGRES_PASSWORD=123456
			
	pgAdmin:
		depends_on:
			- db
		image: dpage/pgadmin4:6.17
		ports:
			- "8080:80"
		volumes:
			- ./pgadmin:/var/lib/pgadmin # Relativo al path
		environment:
			- PGADMIN_DEFAULT_PASSWORD=123456
			- PGADMIN_DEFAULT_EMAIL=superman@google.com
```

```shell
docker compose up
```

Error Linux:
```shell
sudo chown -R 5050:5050 pgadmin
```

### Mongo
```yml
version:'3'

services:
	# Nombre del servicio
	db:
		container_name: ${MONGO_DB_NAME}
		image: mongo:6.0
		volumes:
			- poke-vol:/data/db
		# ports:
		#	- "27017:27017"
		restart: always
		environment:
			- MONGO_INITDB_ROOT_USERNAME: ${MONGO_USERNAME}
			- MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASSWORD}
		command: ['--auth']

	mongo-express:
		depends_on:
			- db
		image: mongo-express:1.0.0-alpha.4
		environment:
			ME_CONFIG_MONGODB_ADMINUSERNAME: ${MONGO_USERNAME}
			ME_CONFIG_MONGODB_ADMINPASSWORD: ${MONGO_PASSWORD}
			ME_CONFIG_MONGODB_SERVER: ${MONGO_DB_NAME}
		ports:
			- "8080:8080"
		restart: always

	poke-app:
		depends_on:
			- db
			- mongo-express
		image: klerith/pokemon-nest-app:1.0.0
		environment:
			MONGODB: mongodb://${MONGO_USERNAME}:${MONGO_PASSWORD}@${MONGO_DB_NAME}:27017
			DBNAME: ${MONGO_DB_NAME}
		ports:
			- "3000:3000"
		restart: always
		

# Crea las imagenes con un volumen que docker determina
volumes:
	poke-vol:
		external: false
```
```.env
MONGO_USERNAME=diego
MONGO_PASSWORD=123456789
MONGO_DB_NAME=pokemonDB
```
