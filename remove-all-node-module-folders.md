# Remove all node_module folders

_Status: Published_
_Created: 2021-07-24 15:41:52_
_Tags: cli, node, npm, node_modules_

```
find . -name "node_modules" -type d -prune | xargs du -chs
```
```
find . -name "node_modules" -type d -prune -exec rm -rf '{}' +
```