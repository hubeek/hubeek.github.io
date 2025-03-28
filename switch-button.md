# Switch Button

_Status: Published_
_Created: 2016-06-07 04:56:21_
_Tags: swift_

<code>
class SwitchButton: UIButton
{
    
    var imageOn:UIImage?
    var imageOff:UIImage?
    var stateOn = true
        {
        didSet
        {
            setImageToState(stateOn)
        }
    }
    
    
    
    //MARK: - VC
    override init(frame: CGRect) {
        super.init(frame: frame)
    }
    
    convenience init(frame: CGRect, imgOn:UIImage, imgOff:UIImage)
    {
        
        self.init(frame: frame)
        
        self.imageOn = imgOn
        self.imageOff = imgOff
        if let img = imageOn as UIImage?
        {
            setImage(img, forState: .Normal)
        }
        self.addTarget(self, action: #selector(SwitchButton.changeState), forControlEvents: UIControlEvents.TouchUpInside)
        
    }
    
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    func changeState()
    {
        self.stateOn = !self.stateOn
    }
    
    func setImageToState(On:Bool)
    {
        switch On {
        case false:
            setImage(imageOff, forState: .Normal)
        default:
            setImage(imageOn, forState: .Normal)
        }
    }
    
}
</code>