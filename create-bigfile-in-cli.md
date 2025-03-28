# create bigfile in cli

_Status: Published_
_Created: 2023-11-16 10:21:59_
_Tags: cli_

create bigfile in cli:
```bash
tr -dc "A-Za-z 0-9" < /dev/urandom | fold -w100|head -n 1000000 > bigfile.txt
```