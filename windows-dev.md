# Windows dev

_Status: Unpublished_
_Created: 2024-05-28 04:29:38_
_Tags: windows, dev_

## nslookup in powershell
```
net user hubeh00 /DOMAIN

net user maatr02 /DOMAIN | findstr IVAD
// kill port
netstat -ano | findstr :<PORT>
taskkill /PID <PID> /F

```
bash
## kill port

```bash
netstat -ano | findstr :<PORT>
taskkill /PID <PID> /F
```

```bash
npx kill-port 9080
```

## set local java to java 11
```
#!/bin/bash
export JAVA_HOME="C:\Program Files\AdoptOpenJDK\jdk-11.0.5.10-hotspot"
# export PATH="${JAVA_HOME}/bin:${PATH}"
# Because of the multiple shells each backslash has to be escaped twice
# so \ becomes \\ becomes \\\\
TEMP_PATH=`echo ${JAVA_HOME} | sed -e "s/\\\\\\\\/\\\\//g" -e "s/^C:/\\\\/c/"`
export PATH="${TEMP_PATH}/bin:${PATH}"
```
# Intellij Hot Reload
in pom.xml
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```
 Ga naar  File | Settings | Build, Execution, Deployment | Compiler
Daar:
vink aan: Build project Automaticly


Dan naar de run configerations:
Ga naar  Select Run/Debug Configuration > Select Edit Configuration 

kies je springboot app
`
Click On Modify options > On 'Update' action
&
On 'Update' Action  Choose > Update recources
&
On frame deactivation > Update classes and recources
(vink upadte classes and resources)
`

