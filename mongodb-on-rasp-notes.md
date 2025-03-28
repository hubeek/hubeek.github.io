# MongoDb on rasp (notes)

_Status: Published_
_Created: 2016-11-23 16:10:34_
_Tags: raspberry pi_

on rasp
sudo /usr/bin/mongod --quiet --rest --config /etc/mongodb.conf
===
sudo nano /etc/mongodb.conf
>
dbpath=/var/lib/mongodb

#where to log
logpath=/var/log/mongodb/mongodb.log

logappend=true

bind_ip = 127.0.0.1,192.168.0.14
port = 27017

# Enable journaling, http://www.mongodb.org/display/DOCS/Journaling
journal=true

# Enables periodic logging of CPU utilization and I/O wait
#cpu = true

in rested

http://192.168.0.14:28017/test/
POST
Accept: */*
Accept-Encoding: gzip, deflate
Content-Type: application/json
Accept-Language: en-us

{
  "user": {
    "email": "blassa4@bbbla.com",
    "pwd": "test4",
    "username": "test4"
  }
}