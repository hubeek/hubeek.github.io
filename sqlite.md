# Sqlite

_Status: Published_
_Created: 2024-07-11 07:24:23_
_Tags: Sqlite_

- ALTER COLUMN is not supported. Official recommendation for changing a column? Make a new table.

- DROP CONSTRAINT is not supported. Official recommendation for removing a constraint? Make a new table.

- SQLite doesn’t have data types on columns. Data types (and there are only five) are on values only, so anything can go anywhere.

- If you ask for a column with an unsupported/non-existent type, it happily does the wrong thing without warning or error. I was raising a schema like CREATE TABLE my_table (id bigserial, messages jsonb[]), which seemed to be working, so I mistakenly thought for the first day that SQLite supported serials and arrays. It does not.

- You can use CREATE TABLE my_table (...) STRICT to only allow one of the five supported types: integer, real, text, blob, any.

- There was a lot of recent fanfare about SQLite’s new support for jsonb. Unlike in Postgres, jsonb is not actually a data type, but rather a format that’s input and output to and from built-in jsonb* functions. When persisted, it’s one of the big five: blob.

Other fairly critical types are also missing. e.g. There’s nothing like timestamptz. If you want a date/time, you store is as a Unix timestamp integer or ISO8601-formatted string, and a number of built-in functions are provided to work with those.

https://brandur.org/atoms/gubk5w2