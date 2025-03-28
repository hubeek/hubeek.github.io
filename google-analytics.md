# Google Analytics

_Status: Published_
_Created: 2015-06-15 03:39:05_
_Tags: swift_

in bridging header
<code>
#import "GAI.h"
#import "GAIFields.h"
#import "GAILogger.h"
#import "GAITracker.h"
#import "GAIDictionaryBuilder.h"
</code>

in appdelegate
<code>
    GAI.sharedInstance().trackUncaughtExceptions = true
    GAI.sharedInstance().dispatchInterval = 20
    GAI.sharedInstance().logger.logLevel = GAILogLevel.Verbose
    GAI.sharedInstance().trackerWithTrackingId("XX-123123123-1")
</code>

event tracker
<code>
    var tracker = GAI.sharedInstance().defaultTracker
    tracker.send(GAIDictionaryBuilder.createEventWithCategory("Button", action: "Pressed", label: "Button", value: nil).build() as [NSObject : AnyObject])
</code>
<p>
<h5>swift 2.0</h5>
<code>
        let appDel = UIApplication.sharedApplication().delegate as! AppDelegate
        let tracker = appDel.tracker //GAI.sharedInstance().defaultTracker
        let eventTracker: NSObject = GAIDictionaryBuilder.createEventWithCategory( "Item bought", action: "bought", label: "itemId", value: 1).build()
        tracker.send(eventTracker as! [NSObject:AnyObject])
</code>
</p>