# Action order for CAKeyframeAnimation

_Status: Published_
_Created: 2018-01-05 09:02:32_
_Tags: swift animation_

Swift 3 
<code>

CATransaction.begin()
CATransaction.setCompletionBlock {
    //Actions to be done after animation
}
//Animation Code
CATransaction.commit()
</code>