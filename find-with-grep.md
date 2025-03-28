# find with grep

_Status: Published_
_Created: 2022-07-17 14:35:35_
_Tags: cli, find_

```
grep -rnw '/path/to/somewhere/' -e 'pattern'
```
include  
```
grep --include=\*.{c,h} -rnw '/path/to/somewhere/' -e "pattern"
```
exclude  
```
grep --exclude=\*.o -rnw '/path/to/somewhere/' -e "pattern"
```
with dir  
```
grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/somewhere/' -e "pattern"
```
