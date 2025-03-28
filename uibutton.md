# uibutton

_Status: Published_
_Created: 2014-10-23 13:11:33_
_Tags: swift_

<code>
    
      let button   = UIButton(type: .Custom)
      button.frame = CGRectMake(100, 100, 100, 50)
      button.backgroundColor = UIColor.greenColor()
      button.setTitle("Button", forState: UIControlState.Normal)
      
      button.addTarget(self, action: #selector(buttonPressed(_:)), forControlEvents: UIControlEvents.TouchUpInside)
      self.addSubview(button)
<code>
