# uiview shape

_Status: Published_
_Created: 2015-05-20 09:58:40_
_Tags: swift_

<code>
override func drawRect(rect: CGRect) {
    

    let context = UIGraphicsGetCurrentContext();
    CGContextSetStrokeColorWithColor(context, strokeColor.CGColor)
    CGContextSetFillColorWithColor(context, fillColor.CGColor)
    CGContextSetLineWidth(context, lineWidth);

    CGContextMoveToPoint(context, (self.frame.width / 2) , lineWidth)
    CGContextAddLineToPoint(context, self.frame.width - lineWidth, self.frame.height - lineWidth)
    CGContextAddLineToPoint(context, lineWidth, self.frame.height - lineWidth)
    CGContextClosePath(context)
    CGContextDrawPath(context, kCGPathFillStroke)
    
    CGContextStrokePath(context)
   
    
  }
</code>