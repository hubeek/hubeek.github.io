# BezierPolygon

_Status: Published_
_Created: 2015-06-19 16:59:41_
_Tags: swift_

<code>
func BezierPolygon(numberOfSides: UInt) -> UIBezierPath {
  let path = UIBezierPath()
  let length : CGFloat = 20.0
  let center = CGPointMake(length, length)
  let radius : CGFloat = length
  var firstPoint = true
  for i in 0..<(numberOfSides - 1) {
    let theta = M_PI + Double(i) * 2.0 * M_PI / Double(numberOfSides)
            let dTheta = 2.0 * M_PI / Double(numberOfSides)
    
    var p = CGPointZero
    if firstPoint {
      p.x = center.x + radius * CGFloat(cos(theta))
      p.y = center.y + radius * CGFloat(sin(theta))
      path.moveToPoint(p)
      firstPoint = false
    }
    
    p.x = center.x + radius * CGFloat(cos(theta + dTheta))
    p.y = center.y + radius * CGFloat(sin(theta + dTheta))
    path.addLineToPoint(p)
  }
  path.closePath()
  return path
}
</code>
from Erica Sadun Playground Secrets and power tips