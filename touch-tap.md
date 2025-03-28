# Touch Tap

_Status: Published_
_Created: 2016-12-01 02:24:31_
_Tags: swift_

<code>
func handleSingleTap(sender:UITapGestureRecognizer){
        print("tapped")
    }
    
    func addTapGesture()
    {
        let singleTap = UITapGestureRecognizer(target:self, action:#selector(handleSingleTap))
        singleTap.numberOfTouchesRequired = 1
        singleTap.addTarget(self, action:#selector(handleSingleTap))
        view.userInteractionEnabled = true
        view.addGestureRecognizer(singleTap)
    }
</code>

or a touch view
<code>
enum Tap {
    case Single
    case Draw
    case Long
    
}

protocol HJHTouchViewDelegate: class{
    func removeSelectedFields()
    func checkThisLoc(pnt:CGPoint)
    func checkThisLocForMove(pnt:CGPoint)
    func touchEnded()
    func longpressAt(pnt:CGPoint)
    func longPressEnd()
}

class TouchView: UIView {
    
    weak var delegate: HJHTouchViewDelegate?
    var tC = 0
    var touchCells = [UIButton]()
    var startTime = NSDate()
    var longPresseTime:Double = 0.5
    var longPressTimer = NSTimer()
    var isInLongPress = false
    var isMoving = false
    
    
    override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?) {
        
        let touch = touches.first!
        tC = 0
        longPressTimer = NSTimer()
        let pnt:CGPoint = touch.locationInView(self)
        delegate?.removeSelectedFields()
        delegate?.checkThisLoc(pnt)
        isInLongPress = false
        isMoving = false
        
        startTime = NSDate()
        longPressTimer =
            NSTimer.scheduledTimerWithTimeInterval(longPresseTime, target: self, selector: #selector(TouchView.updateTime(_:)), userInfo: [pnt.x, pnt.y], repeats: false
        )
        
    }
    
    override func touchesMoved(touches: Set<UITouch>, withEvent event: UIEvent?) {
        isMoving = true
        if isInLongPress
        {
            isInLongPress = false
            delegate?.longPressEnd()
        }
        let touch = touches.first! //as! UITouch
        tC += 1
        let pnt:CGPoint = touch.locationInView(self)
        delegate?.checkThisLocForMove(pnt)
        
    }
    
    
    
    override func touchesEnded(touches: Set<UITouch>, withEvent event: UIEvent?) {
        
        longPressTimer.invalidate()
        isInLongPress = false
        
        delegate?.touchEnded()
    }
    
    func updateTime(timer:NSTimer)
    {
        if isInLongPress ==  true || isMoving == true
        {
            return
        }
        
        if timer.userInfo != nil
        {
            if let info: AnyObject = timer.userInfo
            {
                if isInLongPress == false
                {
                    isInLongPress = true
                    var arr:[CGFloat] = info as! [CGFloat]
                    delegate?.longpressAt( CGPoint(x: arr[0],y: arr[1]))
                }
            }
        }
    }
}
</code>