# MySQL Recap, Stored Procedures

_Status: Published_
_Created: 2021-03-13 11:42:53_
_Tags: mysql, database, sql_

## SQL
Structured query language 

```
show databases;

use dbname;

show tables;

desc users;
```

```
-- use a db
use testdb;

-- use a delimter
delimiter $$

create procedure HelloWorld()
begin
select "Hello WOlrd!";
end$$

delimiter ;

drop procedure HelloWorld;

call HelloWorld();
```