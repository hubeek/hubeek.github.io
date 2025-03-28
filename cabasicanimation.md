# CABasicAnimation

_Status: Published_
_Created: 2018-02-02 06:40:52_
_Tags: iOS swift_

grow shrink, heartbeat?
<code>
let img = UIImage(named: "red_star_2")
let imgv = UIImageView(image: img)
let theAnimation = CABasicAnimation()
theAnimation.keyPath = "transform.scale"
theAnimation.duration = 0.7
theAnimation.repeatCount = .infinity
theAnimation.autoreverses = true
theAnimation.fromValue = 1.0
theAnimation.toValue = 1.3
theAnimation.timingFunction = CAMediaTimingFunction(name: kCAMediaTimingFunctionEaseInEaseOut)
imgv.layer.add(theAnimation, forKey: "animateOpacity")
imgv.center = CGPoint(x: 50, y: 50)
view.addSubview(imgv)</code>
rotation
<code>
let kRotationAnimationKey = "com.myapplication.rotationanimationkey"

let rotationAnimation = CABasicAnimation(keyPath: "transform.rotation")
        rotationAnimation.fromValue = 0.0
        rotationAnimation.toValue = Float(M_PI * 2.0)
        rotationAnimation.duration = 0.2
        rotationAnimation.repeatCount = Float.infinity
        turningStar.layer.add(rotationAnimation, forKey: kRotationAnimationKey)
</code>
with completion
<code>
import UIKit
import PlaygroundSupport

let viewFrame = CGRect(x: 0, y: 0, width: 500, height: 500)
let view = UIView(frame: viewFrame)
view.backgroundColor = .white
PlaygroundPage.current.liveView = view

let v = UIView(frame: CGRect(x: 0, y: 0, width: 20, height: 20))
v.backgroundColor = .red
view.addSubview(v)

CATransaction.begin()
print("start")
let a = CABasicAnimation(keyPath: "position")
a.fromValue = [100, 100]
a.toValue = [200, 200]
a.duration = 2
CATransaction.setCompletionBlock{ print("ended")
}

v.layer.add(a, forKey: nil)
CATransaction.commit()

</code>