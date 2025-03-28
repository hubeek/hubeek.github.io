# Raspberry gpio

_Status: Published_
_Created: 2017-02-18 08:50:44_
_Tags: raspberry pi python_

Read value
<code>
import RPi.GPIO as GPIO

# read value
GPIO.setmode(GPIO.BCM)
GPIO.setup(21, GPIO.IN)
poweron = GPIO.input(21)
GPIO.cleanup(21)
</code>

<code>
 print "turnonheater"
    GPIO.setup(21,GPIO.OUT, initial=GPIO.HIGH)
    GPIO.output(21, GPIO.HIGH)
    GPIO.cleanup(21)
</code>

<code>
 print "turnoffheater"
    GPIO.setup(21,GPIO.OUT, initial=GPIO.LOW)
    GPIO.output(21, GPIO.LOW)
    GPIO.cleanup(21)
</code>