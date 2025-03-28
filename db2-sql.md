# Db2 SQL

_Status: Published_
_Created: 2023-05-14 04:31:15_
_Tags: db2, mysql, sql_

## Like

```
SELECT column1, column2
FROM table_name
WHERE column1 LIKE '%pattern%';
```

Additionally, DB2 supports some additional wildcard characters that can be used with the LIKE operator:

* _ (underscore): Matches any single character. For example, '_at' will match "cat", "bat", but not "at" or "rat".
* [] (brackets): Matches any single character within the specified range or set. For example, '[abc]' will match "a", "b", or "c".
* [^] (caret within brackets): Matches any single character not within the specified range or set. For example, '[^abc]' will match any character except "a", "b", or "c".

```
SELECT column1, column2
FROM table_name
WHERE column1 LIKE 'prefix%';

SELECT column1, column2
FROM table_name
WHERE column1 LIKE '%suffix';

SELECT column1, column2
FROM table_name
WHERE column1 LIKE '%part1_part2%';

SELECT column1, column2
FROM table_name
WHERE column1 LIKE '_at';

SELECT column1, column2
FROM table_name
WHERE column1 LIKE '[abc]at';

SELECT column1, column2
FROM table_name
WHERE column1 LIKE '[^abc]at';
```

## Auto-incrementing Columns:
MySQL uses the AUTO_INCREMENT keyword to define a column that automatically increments its value for each new row inserted into a table.
In DB2, the equivalent functionality is achieved using an identity column, which is defined as GENERATED ALWAYS AS IDENTITY.
## Handling of NULL Values:
MySQL treats NULL values in a unique way when it comes to comparisons and sorting. It considers NULL as the lowest possible value, so NULL values come first when sorting in ascending order and last when sorting in descending order.
DB2 follows the SQL standard behavior for NULL values, where they are considered unknown and are generally sorted at the end regardless of the sorting order.
##  String Comparison and Collation:
MySQL provides various collation options to define how string comparisons should be performed, taking into account factors such as case-sensitivity and accent sensitivity.
DB2 also supports collations for string comparisons, but the default collation is determined by the database and operating system settings. Changing the collation requires altering the database or table collation settings.
## Date and Time Functions:
MySQL and DB2 have some differences in their supported date and time functions.
For example, MySQL provides functions like DATE_FORMAT() for formatting dates, UNIX_TIMESTAMP() for retrieving the current Unix timestamp, and NOW() for obtaining the current date and time.
DB2 uses different functions, such as VARCHAR_FORMAT() for formatting dates, CURRENT_TIMESTAMP for retrieving the current timestamp, and CURRENT DATE for obtaining the current date.
## Pagination Syntax:
When retrieving a limited subset of rows from a query result, MySQL uses the LIMIT clause to specify the number of rows to return and an optional offset to skip rows.
In DB2, the equivalent functionality is achieved using the FETCH FIRST clause along with the ROWS keyword to specify the number of rows to return and the OFFSET clause to skip rows.