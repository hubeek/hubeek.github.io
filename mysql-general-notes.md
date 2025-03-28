# Mysql General notes

_Status: Published_
_Created: 2017-06-09 03:05:34_
_Tags: mysql_

cheat sheet MySQL

<code>
Commands
Access monitor: mysql -u [username] -p; (will prompt for password)

Show all databases: show databases;

Access database: mysql -u [username] -p [database] (will prompt for password)

Create new database: create database [database];

Select database: use [database];

Determine what database is in use: select database();

Show all tables: show tables;

Show table structure: describe [table];

List all indexes on a table: show index from [table];

Create new table with columns: CREATE TABLE [table] ([column] VARCHAR(120), [another-column] DATETIME);

Adding a column: ALTER TABLE [table] ADD COLUMN [column] VARCHAR(120);

Adding a column with an unique, auto-incrementing ID: ALTER TABLE [table] ADD COLUMN [column] int NOT NULL AUTO_INCREMENT PRIMARY KEY;

Inserting a record: INSERT INTO [table] ([column], [column]) VALUES ('[value]', [value]');

MySQL function for datetime input: NOW()

Selecting records: SELECT * FROM [table];

Explain records: EXPLAIN SELECT * FROM [table];

Selecting parts of records: SELECT [column], [another-column] FROM [table];

Counting records: SELECT COUNT([column]) FROM [table];

Counting and selecting grouped records: SELECT *, (SELECT COUNT([column]) FROM [table]) AS count FROM [table] GROUP BY [column];

Selecting specific records: SELECT * FROM [table] WHERE [column] = [value]; (Selectors: <, >, !=; combine multiple selectors with AND, OR)

Select records containing [value]: SELECT * FROM [table] WHERE [column] LIKE '%[value]%';

Select records starting with [value]: SELECT * FROM [table] WHERE [column] LIKE '[value]%';

Select records starting with val and ending with ue: SELECT * FROM [table] WHERE [column] LIKE '[val_ue]';

Select a range: SELECT * FROM [table] WHERE [column] BETWEEN [value1] and [value2];

Select with custom order and only limit: SELECT * FROM [table] WHERE [column] ORDER BY [column] ASC LIMIT [value]; (Order: DESC, ASC)

Updating records: UPDATE [table] SET [column] = '[updated-value]' WHERE [column] = [value];

Deleting records: DELETE FROM [table] WHERE [column] = [value];

Delete all records from a table (without dropping the table itself): DELETE FROM [table]; (This also resets the incrementing counter for auto generated columns like an id column.)

Delete all records in a table: truncate table [table];

Removing table columns: ALTER TABLE [table] DROP COLUMN [column];

Deleting tables: DROP TABLE [table];

Deleting databases: DROP DATABASE [database];

Custom column output names: SELECT [column] AS [custom-column] FROM [table];

Export a database dump (more info here): mysqldump -u [username] -p [database] > db_backup.sql

Use --lock-tables=false option for locked tables (more info here).

Import a database dump (more info here): mysql -u [username] -p -h localhost [database] < db_backup.sql

Logout: exit;

Aggregate functions
Select but without duplicates: SELECT distinct name, email, acception FROM owners WHERE acception = 1 AND date >= 2015-01-01 00:00:00

Calculate total number of records: SELECT SUM([column]) FROM [table];

Count total number of [column] and group by [category-column]: SELECT [category-column], SUM([column]) FROM [table] GROUP BY [category-column];

Get largest value in [column]: SELECT MAX([column]) FROM [table];

Get smallest value: SELECT MIN([column]) FROM [table];

Get average value: SELECT AVG([column]) FROM [table];

Get rounded average value and group by [category-column]: SELECT [category-column], ROUND(AVG([column]), 2) FROM [table] GROUP BY [category-column];

Multiple tables
Select from multiple tables: SELECT [table1].[column], [table1].[another-column], [table2].[column] FROM [table1], [table2];

Combine rows from different tables: SELECT * FROM [table1] INNER JOIN [table2] ON [table1].[column] = [table2].[column];

Combine rows from different tables but do not require the join condition: SELECT * FROM [table1] LEFT OUTER JOIN [table2] ON [table1].[column] = [table2].[column]; (The left table is the first table that appears in the statement.)

Rename column or table using an alias: SELECT [table1].[column] AS '[value]', [table2].[column] AS '[value]' FROM [table1], [table2];

Users functions
List all users: SELECT User,Host FROM mysql.user;

Create new user: CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

Grant ALL access to user for * tables: GRANT ALL ON database.* TO 'user'@'localhost';

Find out the IP Address of the Mysql Host
SHOW VARIABLES WHERE Variable_name = 'hostname'; (source)
</code>
<h2>Sizes databases</h2>
<code>
SELECT table_schema AS "Database", 
ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS "Size (MB)" 
FROM information_schema.TABLES 
GROUP BY table_schema;
</code>
index, indices, indexes
<code>
alter table book add index idx_name(name)
alter table book drop index idx_name
</code>
multiple row updates at same time
<code>
set sql_save_updates=0
</code>
check
<code>
SHOW VARIABLES LIKE 'sql_safe_updates'
</code>
renumber id column
<code>
SET @i=0;
UPDATE table_name SET column_name=(@i:=@i+1);
</code>
<code>
set @rank=0;select @rank:=@rank+1 as rank , screenname, score from gameScore order by score desc;
</code>
<code>
select groep , screenname from user where userGroup.groep < 98 order by groep;
</code>

<h2>Explain Select</h2>
<code>
explain select  count(*) from `tuinhokmetingen`.`AspNetUsers`;
</code>

<h2>Show create</h2>
<code>
show create TABLE `temperatures`;
</code>
