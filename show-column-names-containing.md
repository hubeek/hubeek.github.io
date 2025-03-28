# show column names containing %..%

_Status: Published_
_Created: 2014-05-31 17:48:29_
_Tags: mysql_

show column names met naam %rekening%

SELECT table_name, column_name
FROM information_schema.columns
WHERE column_name LIKE '%rekening%'
LIMIT 0 , 30