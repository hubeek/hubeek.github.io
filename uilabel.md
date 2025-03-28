# uilabel

_Status: Published_
_Created: 2014-10-23 13:14:39_
_Tags: swift_

<code>    
var label: UILabel = UILabel()
label.frame = CGRectMake(50, 50, 200, 21)
label.backgroundColor = UIColor.blackColor()
label.textColor = UIColor.whiteColor()
label.textAlignment = NSTextAlignment.Center
label..numberOfLines = 0
label.text = "test label"
self.view.addSubview(label)
</code>

<h3>Multiline</h3>
<code>
label.lineBreakMode = .ByWordWrapping 
label.numberOfLines = 0 
</code>