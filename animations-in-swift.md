# Animations in swift

_Status: Published_
_Created: 2015-03-08 03:39:44_
_Tags: swift_

<h2>Music bars moving</h2>
<code>
func animationMusicBars() {
    let r = CAReplicatorLayer()
    r.bounds = CGRect(x: 0.0, y: 0.0, width: 60.0, height: 60.0)
    r.position = CGPoint(x: 60, y: 60)
    view.layer.addSublayer(r)
    
    let bar = CALayer()
    bar.bounds = CGRect(x: 0.0, y: 0.0, width: 8.0, height: 40.0)
    bar.position = CGPoint(x: 10.0, y: 75.0)
    bar.cornerRadius = 2.0
    bar.backgroundColor = UIColor.redColor().CGColor
    
    r.addSublayer(bar)
    
    let move = CABasicAnimation(keyPath: "position.y")
    move.toValue = bar.position.y - 35.0
    move.duration = 0.5
    move.autoreverses = true
    move.repeatCount = Float.infinity
    
    bar.addAnimation(move, forKey: nil)
    
    r.instanceCount = 6
    r.instanceTransform = CATransform3DMakeTranslation(9.0, 0.0, 0.0)
    r.instanceDelay = 0.13
    r.masksToBounds = true
    
  }
</code>
<br />
<h2>Spinning Blocks</h2>
<code>
func animationSpingBlocks(){
    let r = CAReplicatorLayer()
    r.bounds = CGRect(x: 0.0, y: 0.0, width: 200.0, height: 200.0)
    r.cornerRadius = 10.0
    r.backgroundColor = UIColor(white: 0.0, alpha: 0.75).CGColor
    r.position = CGPoint(x: 220, y: 120)
    
    view.layer.addSublayer(r)
    
    let dot = CALayer()
    dot.bounds = CGRect(x: 0.0, y: 0.0, width: 14.0, height: 14.0)
    dot.position = CGPoint(x: 100.0, y: 40.0)
    dot.backgroundColor = UIColor(white: 0.8, alpha: 1.0).CGColor
    dot.borderColor = UIColor(white: 1.0, alpha: 1.0).CGColor
    dot.borderWidth = 1.0
    dot.cornerRadius = 2.0
    
    r.addSublayer(dot)
    
    let nrDots: Int = 15
    
    r.instanceCount = nrDots
    let angle = CGFloat(2*M_PI) / CGFloat(nrDots)
    r.instanceTransform = CATransform3DMakeRotation(angle, 0.0, 0.0, 1.0)
    
    let duration: CFTimeInterval = 1.5
    
    let shrink = CABasicAnimation(keyPath: "transform.scale")
    shrink.fromValue = 1.0
    shrink.toValue = 0.1
    shrink.duration = duration
    shrink.repeatCount = Float.infinity
    
    dot.addAnimation(shrink, forKey: nil)
    r.instanceDelay = duration/Double(nrDots)
    dot.transform = CATransform3DMakeScale(0.01, 0.01, 0.01)
  
  }
</code>
source: http://www.ios-animations-by-emails.com/posts/2015-march#tutorial