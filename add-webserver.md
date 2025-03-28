# add webserver

_Status: Published_
_Created: 2014-08-18 13:12:57_
_Tags: raspberry pi_

<H1>Installing The Web Server</H1>

sudo apt-get install apache2 php5 libapache2-mod-php5

restart:
sudo service apache2 restart
OR
sudo /etc/init.d/apache2 restart

Enter the I.P. address of your Raspberry Pi into your web browser. You should see a simple page that says "It Works!"

<H1>Install MySQL</H1>

sudo apt-get install mysql-server mysql-client php5-mysql


<H1>Install FTP</H1>
Take ownership of the web root:
sudo chown -R pi /var/www

 install vsftpd:
sudo apt-get install vsftpd

sudo nano /etc/vsftpd.conf

Make the following changes:
<ul>anonymous_enable=YES to anonymous_enable=NO</ul>
<ul>Uncomment local_enable=YES and write_enable=YES by deleting the # symbol in front of each line</ul>
<ul>then go to the bottom of the file and add force_dot_files=YES.</ul>

sudo service vsftpd restart

ln -s /var/www/ ~/www