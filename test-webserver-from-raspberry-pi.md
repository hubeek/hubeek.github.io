# Test Webserver from raspberry pi

_Status: Published_
_Created: 2016-07-17 17:48:39_
_Tags: raspberry pi_

<code>
import smtplib
import httplib
import datetime

GMAIL_USER = 'email@gmail.com'
GMAIL_PASS = 'password'
SMTP_SERVER = 'smtp.gmail.com'
SMTP_PORT = 587

def send_email(recipient, subject, text):
    smtpserver = smtplib.SMTP(SMTP_SERVER, SMTP_PORT)
    smtpserver.ehlo()
    smtpserver.starttls()
    smtpserver.ehlo
    smtpserver.login(GMAIL_USER, GMAIL_PASS)
    header = 'To:' + recipient + '\n' + 'From: ' + GMAIL_USER
    header = header + '\n' + 'Subject:' + subject + '\n'
    msg = header + '\n' + text + ' \n\n'
    smtpserver.sendmail(GMAIL_USER, recipient, msg)
    smtpserver.close()

def get_status_code(host, path="/"):
    """ This function retreives the status code of a website by requesting
        HEAD data from the host. This means that it only requests the headers.
        If the host cannot be reached or something else goes wrong, it returns
        None instead.
    """
    try:
        conn = httplib.HTTPConnection(host)
        conn.request("HEAD", path)
        return conn.getresponse().status
    except StandardError:
        return None   

if  get_status_code("site.com") != 200:
    f = open("/home/pi/servertest/logfile.txt", "a")
    f.write(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") + ' status != 200 ERROR' + '\n' )
    f.close()
    print "something wrong"
    send_email('email@gmail.com', 'server not at 200', 'server not at 200')
    
else:
    f = open("/home/pi/servertest/logfile.txt", "a")
    f.write(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") + ' status == 200' + '\n' )
    f.close()
    print "status == 200"
</code>
add cron to crontab
<code>
crontab -e
</code>

test every 10 minutes
<code>
*/10     *      *     *    *   python  /home/pi/servertest/servertest.py
</code>


to start cron
<code>
sudo service cron start
</code>