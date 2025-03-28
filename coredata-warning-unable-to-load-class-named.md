# CoreData: warning: Unable to load class named

_Status: Published_
_Created: 2015-03-19 07:55:03_
_Tags: swift_

1.
<img src="http://i.stack.imgur.com/f3vo5.png">
enter image description here

Notice that I corrected your entity name to the more appropriate singular.

2.
You should also follow the frequent recommendation to include

@objc(Show)
just above your class.

3.
Also make sure to cast the created managed object to the proper class, as the default would be just NSManagedObject.

var newShow = NSEntityDescription.insertNewObjectForEntityForName("Show", 
                 inManagedObjectContext: context) as Show