# Windows cli check for running at port 1234

_Status: Published_
_Created: 2020-10-21 09:35:59_
_Tags: windows, cli, terminal, bash, javascript, angular_

```
netstat -ano | findstr :<PORT>
tskill typeyourPIDhere 
or taskkill /PID 14328 /F
```