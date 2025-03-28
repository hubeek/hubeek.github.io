# tweenlite

_Status: Published_
_Created: 2014-10-06 09:28:40_
_Tags: Actionscript_

//import the GreenSock classes
import com.greensock.*;
import com.greensock.easing.*;

//tween the MovieClip named "mc" to an alpha of 0.5 over the course of 3 seconds
<code>TweenLite.to(mc, 3, {alpha:0.5});</code>
//scale myButton to 150% (scaleX/scaleY of 1.5) using the Elastic.easeOut ease for 2 seconds
<code>TweenLite.to(myButton, 2, {scaleX:1.5, scaleY:1.5, ease:Elastic.easeOut});</code>
//tween mc3 in FROM 100 pixels above wherever it is now, and an alpha of 0. (notice the vars object defines the starting values instead of the ending values)
<code>TweenLite.from(mc3, 1, {y:"-100", alpha:0});</code>
//after a delay of 3 seconds, tween mc for 5 seconds, sliding it across the screen by changing its "x" property to 300, using the Back.easeOut ease to make it shoot past it and come back, and then call the onFinishTween() function, passing two parameters: 5 and mc
<code>TweenLite.to(mc, 5, {delay:3, x:300, ease:Back.easeOut, onComplete:onFinishTween, onCompleteParams:[5, mc]});</code>
<code>function onFinishTween(param1:Number, param2:MovieClip):void {</code>
<code>trace("The tween has finished! param1 = "   param1   ", and param2 = "   param2);</code>
<code>}</code>
//call myFunction() after 2 seconds, passing 1 parameter: "myParam"
<code>TweenLite.delayedCall(2, myFunction, ["myParam"]);</code>
//use the object-oriented syntax to create a TweenLite instance and store it so we can reverse, restart, or pause it later.
<code>var myTween:TweenLite = new TweenLite(mc2, 3, {y:200, alpha:0.5, onComplete:myFunction});</code>
//some time later (maybe in by a ROLL_OUT event handler for a button), reverse the tween, causing it to go backwards to its beginning from wherever it is now.
<code>myTween.reverse();</code>
//pause the tween
<code>myTween.pause();</code>
//restart the tween
<code>myTween.restart();</code>
//make the tween jump to exactly its 2-second point
<code>myTween.currentTime = 2;</code>