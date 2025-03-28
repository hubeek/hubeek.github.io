# raspi config ssh problem

_Status: Published_
_Created: 2017-10-14 06:24:52_
_Tags: raspberry pi bash python_

ssh pi@192.168.1.27
Connection reset by 192.168.1.27 port 22
solution:
<code>
sudo rm /etc/ssh/ssh_host_* && sudo dpkg-reconfigure openssh-server
</code>