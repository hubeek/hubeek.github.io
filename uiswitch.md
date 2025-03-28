# uiswitch

_Status: Published_
_Created: 2015-01-28 16:47:57_
_Tags: swift_

<code>
mainSwitch = UISwitch(frame: CGRect(x: 100, y: 100, width: 0, height: 0))
    
    /* Adjust the off-mode tint color */
    mainSwitch.tintColor = UIColor.redColor()
    /* Adjust the on-mode tint color */
    mainSwitch.onTintColor = UIColor.brownColor()
    /* Also change the knob's tint color */
    mainSwitch.thumbTintColor = UIColor.greenColor()
    
    view.addSubview(mainSwitch)

@IBAction func soundEffectsSwitchChanged(sender: UISwitch) {
    
    if sender.on {
      
      Settings().setSoundFx(true)
    
    } else {
      
      Settings().setSoundFx(false)
    }
  }
</code>