# nsnotificaton

_Status: Published_
_Created: 2015-03-26 03:35:09_
_Tags: swift_

<h2>Sent(Post) Notification</h2>
<code>
NSNotificationCenter.defaultCenter().postNotificationName("NotificationIdentifier", object: nil)
</code>
<h2>Receive(Get) Notification</h2>
<code>
NSNotificationCenter.defaultCenter().addObserver(self, selector: "methodOfReceivedNotification:", name:"NotificationIdentifier", object: nil)
</code>
<h2>Remove Notification</h2>
<code>
NSNotificationCenter.defaultCenter().removeObserver(self, name: "NotificationIdentifier", object: nil)
</code>
<h2>Method of received Notification</h2>

<code>
func methodOfReceivedNotification(notification: NSNotification){
    //Action take on Notification
}
</code>