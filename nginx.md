# Nginx

_Status: Published_
_Created: 2017-06-21 17:18:05_

<code>
apt-get update
apt-get install nginx
service nginx start
</code>

Download the init script for the relevant platform and save it to /etc/rc.d/init.d/nginx
chmod +x /etc/rc.d/init.d/nginx

directives and context

search & analytics nginx

nginx
/var/log/nginx

cat access.log | awk '{print $7}' | sort -rn | uniq -c

ips in log
cat access.log | grep xmlrpc | awk '{print $1}' | sort -n | uniq

per req uri
cat /var/log/nginx/access.log | awk '{print $11}' | sort | uniq -c | sort -n

problems with server restart
/usr/sbin/nginx
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)

<code>
sudo apachectl stop
sudo pkill -f nginx
sudo systemctl start nginx
</code>