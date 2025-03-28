# General

_Status: Published_
_Created: 2014-08-18 13:03:09_
_Tags: raspberry pi_

##Update
sudo apt update -y && apt upgrade -y 
 

##Reboot
```sudo shutdown -h now (or sudo reboot)```


## Locale
edit ~/.bashrc
add
LANG="en_US.UTF-8"



##temperature sensor

sudo modprobe w1-gpio
sudo modprobe w1-therm
ls /sys/bus/w1/devices

```temp sensor not visible in /sys/bus/w1/devices```
```
sudo nano /boot/config.txt
```
add :
```
dtoverlay=w1-gpio
```