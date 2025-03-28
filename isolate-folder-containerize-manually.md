# Isolate folder containerize manually

_Status: Published_
_Created: 2021-06-29 02:29:35_
_Tags: linux, cli, container, isolation_

in linux env
```
mkdir jail  
sudo cp /bin/bash ./jail/  
tree jail  
ldd /bin/bash # see the dep of bash program  
mkdir /jail/lib64  
sudo cp /lib64/lininfo.so.6 jail/lib64 // etc 5c  
tree jail  
chroot /root/jail/ ./bash // !!!  
```