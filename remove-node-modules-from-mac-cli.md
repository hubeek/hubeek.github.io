# remove node_modules from mac cli

_Status: Published_
_Created: 2021-06-07 12:02:35_

## find
```
find -d .  -name node_modules -prune 
```

## find & size  
```
Development % find . -type d -name node_modules -prune | tr '\n' '\0' |  xargs -0 du -sch  
```
  
  
## find & remove  
```
find . -name "node_modules" -type d -prune -exec rm -rf '{}' +  
```