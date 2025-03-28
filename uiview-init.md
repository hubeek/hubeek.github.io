# UIView init

_Status: Published_
_Created: 2016-06-07 09:26:51_
_Tags: swift_

<code>
class AView:UIView
{
    override init(frame: CGRect) {
        super.init(frame: frame)
        
        self.initialize()
    }
    
    convenience init() {
        self.init(frame: CGRectZero)
        
        self.initialize()
    }
    
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    func initialize() {
        doAFunc()
    }
}
</code>