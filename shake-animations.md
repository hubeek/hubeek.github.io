# shake animations

_Status: Published_
_Created: 2017-11-15 08:43:49_
_Tags: swift_

<code>
func shakeByRotateView(view:UIView){
    let shake:CABasicAnimation = CABasicAnimation(keyPath: "transform.rotation")
    shake.duration = 0.12
    shake.repeatCount = Float.infinity
    shake.autoreverses = true
    
    shake.fromValue = NSNumber(value: 0.05*Double.pi)
    shake.toValue = NSNumber(value: -0.05*Double.pi)
    view.layer.add(shake, forKey: "lineRotation")
}
</code>

<code>
func shakeView(view:UIView){
    let shake:CABasicAnimation = CABasicAnimation(keyPath: "position")
    shake.duration = 0.1
    shake.repeatCount = 2
    shake.autoreverses = true
    
    var from_point:CGPoint = CGPoint(x:view.center.x - 5,y: view.center.y)
    var from_value:NSValue = NSValue(cgPoint: from_point)
    
    var to_point:CGPoint = CGPoint(x:view.center.x + 5,y: view.center.y)
    var to_value:NSValue = NSValue(cgPoint: to_point)
    
    shake.fromValue = from_value
    shake.toValue = to_value
    view.layer.add(shake, forKey: "position")
}
</code>