# Record crashes

_Status: Published_
_Created: 2015-11-24 05:46:24_
_Tags: swift_

<p>General func</p>
<code>
func exceptionHandler(exception : NSException) {
  let defaults: NSUserDefaults = NSUserDefaults.standardUserDefaults()
  
 
    defaults.setObject(exception.debugDescription , forKey: "exception")
    defaults.synchronize()
  print("exc: \(exception)")
  print("exc call stack: \(exception.callStackSymbols)")
}
</code>
<br />
<p>in didFinishLaunchingWithOptions</p>
<code>
NSSetUncaughtExceptionHandler(exceptionHandler)
    if NSUserDefaults.standardUserDefaults().objectForKey("exception") != nil
    { .. }
</code>

<br />
<p>
create crash for example with
</p>
<code>
let array = NSArray()
let elem = array.objectAtIndex(99)
</code>