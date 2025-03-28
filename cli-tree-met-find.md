# cli tree met find

_Status: Published_
_Created: 2022-10-14 09:32:32_
_Tags: cli, tree, find_

## find
```
find -maxdepth 2 -type d -ls | sed -e 's/[^-][^\/]*\//--/g' -e 's/^/ /' > tree.txt
```
in tree text file  
 --test  
 ----test.git  
 --apps  
 ----namefile1.git  
 ----namefile2.git  

## ls
```
ls -R | grep ":$" | sed -e 's/:$//' -e 's/[^-][^\/]*\//--/g' -e 's/^/ /' -e 's/-/|/'
```
 |-folder  
 |---dir  
 |---dir2  