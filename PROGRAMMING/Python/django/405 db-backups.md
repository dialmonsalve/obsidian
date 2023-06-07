
### Postgres
```shell
mkdir backupdb # Create dir
chmod 777 backupdb # Set permissions
cd backupdb
sudo postgres

#Inside postgres shell
pg_dump dbname > name_copy
dropdb dbname # Remove db
createdb dbname # Create a new db
psql dbname
alter user usename with password 'password'
\q # Close postgres shell query
psql dbname < name_copy

#Finally in python delete all 0001_initial.py migrations
# Create a fake migrations
python manage.py migrate --fake
```