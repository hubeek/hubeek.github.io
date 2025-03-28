# Conda

_Status: Published_
_Created: 2023-03-17 03:06:44_

search on system:
```
conda search "^python$"
```
or
```
conda list | grep "^python"
```

```
conda create --name py311 python=3.11
conda config --set default_env py311
```
```
conda activate py311
```
check what version
```
python -V
pip -V
```
pip  upgrade
```
pip install -U pip
```
