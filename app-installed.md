# App installed

_Status: Published_
_Created: 2017-02-22 04:14:15_
_Tags: iOS_

<code>
func isAppInstalled(name:String)->Bool {
    return UIApplication.sharedApplication().canOpenURL(NSURL(string:"\(name):")!)
}
</code>