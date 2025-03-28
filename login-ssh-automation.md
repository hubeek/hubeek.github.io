# Login ssh automation

_Status: Published_
_Created: 2019-11-24 09:11:03_
_Tags: python, zsh, terminal_

```
import sys
import pyperclip
import subprocess

if len(sys.argv) == 1:
    print('login func needs client to login...')
elif sys.argv[1] == 'do':
    print('login at do, use paste')
    cb = pyperclip.copy('Password')
    bashCommand = "echo apt update"
    subprocess.call(["ssh", "user@ip.address.0.0"])
else:
    print('No login available for '+ sys.argv[1])

sys.exit(1)
```
adjust zshrc
in 


~/.zshrc
add location python3 and filelocation
```
alias li="/Users/hjhubeek/Documents/development/python/li/bin/python /Users/hjhubeek/Documents/development/python/li/li.py"
```