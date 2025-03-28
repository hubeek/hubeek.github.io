# minecraft raspberry server

_Status: Published_
_Created: 2016-06-07 04:55:37_
_Tags: minecraft raspberry server_

sudo apt-get update && sudo apt-get install oracle-java7-jdk 
or
sudo apt-get update && sudo apt-get install oracle-java8-jdk

https://s3.amazonaws.com/Minecraft.Download/versions/1.9/minecraft-server.1.9.jar

or
https://minecraft.net/download

java -Xmx1G -Xms1G -jar minecraft_server.1.9.jar -nogui


========


java -Xms512m -Xmx2048m -jar craftbukkit.jar nogui