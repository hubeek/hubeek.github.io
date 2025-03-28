# GCD

_Status: Published_
_Created: 2015-03-26 05:58:59_
_Tags: swift_

<h2>After amount of time</h2>
<code>
func delay(delay:Double, closure:()->()) {
    dispatch_after(
        dispatch_time(
            DISPATCH_TIME_NOW,
            Int64(delay * Double(NSEC_PER_SEC))
        ),
        dispatch_get_main_queue(), closure)
}
</code>
so use it as:
<code>
delay(0.4) {
    // do stuff
}
</code>

<b>swift 3</b>
<code>
func delay(delay:Double, closure:()->Void) {
  DispatchQueue.main.after(when: DispatchTime.now()+delay, execute: closure)
}
</code>