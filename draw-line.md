# Draw Line

_Status: Published_
_Created: 2015-04-05 10:15:15_
_Tags: swift_

<code>
UIColor.brownColor().set()
  let context = UIGraphicsGetCurrentContext()
  CGContextSetLineWidth(context, 5)
  CGContextMoveToPoint(context, 50, 10)
  CGContextAddLineToPoint(context, 100, 123)
  CGContextStrokePath(context)
</code>