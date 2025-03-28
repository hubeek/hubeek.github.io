# Brew

_Status: Published_
_Created: 2023-07-22 03:58:54_
_Tags: cli, brew_

```bash
brew list
```
## View Dep tree</h2>
```bash
for package in $(brew leaves); do echo $package; brew deps $package; echo; done 
```
## Leaves
List top-level installed packages  

```bash
brew leaves
```
with sizes:
```bash
brew list --formula | while read cask; do echo -n "$cask: "; du -sh $(brew --prefix)/Cellar/$cask; done
```


## Update & Upgrade
```bash
brew update && brew upgrade 
```

## Brew Info
```bash
brew info 
```
