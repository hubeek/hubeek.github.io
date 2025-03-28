# Tarsnap

_Status: Published_
_Created: 2022-05-21 18:11:33_

### Setup
create tarsnap key file in root folder.   
So there will be a /root/ folder with the key in there.  
For Mac this is problematic while / is read-only, thus:
create a /etc/synthetic.conf
```
root    Users/username/tarsnap
```
Then reboot and the folder and its link wil be made.

### List
```sudo tarsnap --list-archives | sort ```

### Delete
```
sudo tarsnap -d -f <filename>
```
### Backup script  
backupscript.sh
```
#!/bin/sh
/usr/local/bin/tarsnap -c \
        -f "$(uname -n)-$(date +%Y-%m-%d_%H-%M-%S)" \
        /Users/username/dirToBackup
```
### Dry run

for file size check  
```
tarsnap --dry-run --no-default-config --print-stats --humanize-numbers -c /Users/username/dirname
```


