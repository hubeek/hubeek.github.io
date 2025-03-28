# attributes text with smart range

_Status: Published_
_Created: 2015-01-28 16:34:42_
_Tags: swift_

<code>

    let string = "iOS SDK" as NSString
    
    let result = NSMutableAttributedString(string: string)
    
    let attributesForFirstWord = [
      NSFontAttributeName : UIFont.boldSystemFontOfSize(60),
      NSForegroundColorAttributeName : UIColor.redColor(),
      NSBackgroundColorAttributeName : UIColor.blackColor()
    ]
    
    let shadow = NSShadow()
    shadow.shadowColor = UIColor.darkGrayColor()
    shadow.shadowOffset = CGSize(width: 4, height: 4)
    
    let attributesForSecondWord = [
      NSFontAttributeName : UIFont.boldSystemFontOfSize(60),
      NSForegroundColorAttributeName : UIColor.whiteColor(),
      NSBackgroundColorAttributeName : UIColor.redColor(),
      NSShadowAttributeName : shadow,
    ]
    
    /* Find the string "iOS" in the whole string and sets its attribute */
    result.setAttributes(attributesForFirstWord,
      range: string.rangeOfString("iOS"))
    
    
    /* Do the same thing for the string "SDK" */
    result.setAttributes(attributesForSecondWord,
      range: string.rangeOfString("SDK"))

</code>