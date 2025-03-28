# json call rest

_Status: Published_
_Created: 2014-12-19 16:04:26_
_Tags: python_

import urllib, json
>>> url = "http://maps.googleapis.com/maps/api/geocode/json?address=googleplex&sensor=false"
>>> url = "http://myexternalip.com/json"
>>> response = urllib.urlopen(url);
>>> data = json.loads(response.read())
>>> print data
{u'ip': u'80.57.121.251'}