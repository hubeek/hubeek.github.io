# Docker dbs

_Status: Published_
_Created: 2023-03-09 13:15:21_

## Mongo Db
```
docker pull mongo
docker run -d --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=mypassword mongo
```
## Postgres Db
```
docker run --name postgresdb -p 5432:5432 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=secret -d postgres
docker run --name pgadmin -p 8080:80 -e 'PGADMIN_DEFAULT_EMAIL=user@domain.com' -e 'PGADMIN_DEFAULT_PASSWORD=secret' -d dpage/pgadmin4

```
## MySQL Db
```
docker run --name mysql-db -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql
```
Use:
```
docker exec -it postgres psql -U postgres
docker exec -it mongosh
```