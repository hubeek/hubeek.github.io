# background color to image

_Status: Published_
_Created: 2015-03-03 03:43:31_
_Tags: swift_

<code>
self.view.backgroundColor = UIColor(patternImage: UIImage(named: "background.png"))
</code>

<p>
UIView:
<code>
let banner = UIView(frame: CGRectMake(x, y, width, height))

UIGraphicsBeginImageContext(banner.frame.size)
UIImage(named: "banner_promo")?.drawInRect(banner.bounds)
var image: UIImage = UIGraphicsGetImageFromCurrentImageContext()
UIGraphicsEndImageContext()
banner.backgroundColor = UIColor(patternImage: image)
</code>
</p>