# size databases 

_Status: Published_
_Created: 2017-01-12 14:44:35_
_Tags: mysql_

<code>
SELECT table_schema AS `Database`, 
SUM(data_length + index_length) / 1024 / 1024 AS `Size in MB` 
FROM information_schema.TABLES 
GROUP BY table_schema;
</code>