# combine adding CGRects in array

_Status: Published_
_Created: 2017-07-19 10:23:46_
_Tags: swift_

Adding two CGRect:
<code>
let area0 = CGRectZero //{x 0 y 0 w 0 h 0}
let area1 = CGRect(x:0,y:0,width: 2.0, height: 2.0)//{x 0 y 0 w 2 h 2}
let area2 = CGRect(x:2.0,y:2.0,width: 2.0, height: 2.0)
let area3 = CGRect(x:4.0,y:4.0,width: 2.0, height: 2.0)
let union = CGRectUnion(area1, area2)//{x 0 y 0 w 4 h 4}
</code>
in an array
<code>

var areatotal:[CGRect] = []
areatotal.append(area1)
areatotal.append(area2)
areatotal.append(area3)
areatotal.append(area0)
areatotal.reduce(CGRectZero, combine: CGRectUnion)//{x 0 y 0 w 6 h 6}
</code>