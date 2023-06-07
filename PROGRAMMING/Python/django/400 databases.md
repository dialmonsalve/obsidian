
## Database configurations

##### **PostgreSQL** 
Configure [user](403%20user_postgres.md)
```shell
pip install psycopg2 # windows
```
```shell
pip install psycopg-binary # linux
```
```python
DATABASES ={
		'default': {
				'ENGINE'  : 'django.db.backends.postgresql',
				'NAME'    : 'nombre_bd',
				'USER'    : 'usuario_postgresql',
				'PASSWORD': 'password_postgresql',
				'HOST'    : 'localhost',
				'PORT'    : 5432
		}
}
``` ^4217bb
- To install triagram in postgreSQL for advance queries, configure db first
	- Install Linux
		```shell
	sudo apt-get install postgresql-contrib
	sudo psql db
	dbDatabasePost=# CREATE EXTENSION pg_trgm;
	dbDatabasePost=# CREATE INDEX index_name ON app_model USING GIN(field gin_trgm_ops);
	CREATE INDEX # Shows this message if all go good
```
When all is OK, configure [[404 Query Managers#Trigram|trigram]] in django

#### **MYSQL**
```shell
pip install mysqlclient
```

```python
DATABASE ={
		'default': {
				'ENGINE'  : 'django.db.backends.mysql',
				'NAME'    : 'nombre_bd',
				'USER'    : 'usuario_root',
				'PASSWORD': 'password_root',
				'HOST'    : 'localhost',
				'PORT'    : 3306
		}
}
``` 

#### Common queries
Here are some of the most [common queries](401%20database_queries.md) in Django models

Here there are the most [common fields](402%20field_type_django_models.md) in Django models

#### Backup:
##### Create data
```shell
python manage.py dumpdata > file.json
```

##### Load data
```shell
	python manage.py loaddata file.json
```

##### Restart db 
```shell
	python manage.py flux
```
