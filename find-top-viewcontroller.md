# find top viewcontroller

_Status: Published_
_Created: 2016-03-10 10:14:35_
_Tags: swift_

<code>
extension UIApplication {
  class func topViewController(base: UIViewController? = (UIApplication.sharedApplication().delegate as! AppDelegate).window?.rootViewController) -> UIViewController? {
    if let nav = base as? UINavigationController {
      return topViewController(nav.visibleViewController)
    }
    if let tab = base as? UITabBarController {
      if let selected = tab.selectedViewController {
        return topViewController(selected)
      }
    }
    if let presented = base?.presentedViewController {
      return topViewController(presented)
    }
    return base
  }
}
</code>
<br />
<br />
<p>
and use like
</p>
<code>
if let topvc = UIApplication.topViewController()
          {
            if topvc is HomeVC
            {
              let vc = topvc as! HomeVC
              vc.updateGcmMessageButton()
            }
          }
</code>