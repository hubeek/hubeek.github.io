# Shuffle

_Status: Published_
_Created: 2016-09-03 16:24:02_
_Tags: swift_

Fisher–Yates shuffle<br />
<code>
func shuffle<T>(arr:[T]) ->[T]
{
    var array:[T] = arr
    var m = array.count
    var t :T
    var i = 0
    
    while (m > 0) {
        
        m -= 1
        i = Int(arc4random_uniform(UInt32(m)))
        
        t = array[m]
        array[m] = array[i]
        array[i] = t
    }
    
    return array
}
</code>

with gameplaykit
then NSArray has extended func .shuffled()
<code>
import GameplaKit
(array as NSArray).shuffled()
</code>
or with GKRandomSource
<code>
import GameplayKit

var arr = [1,2,3,4,5,6,7]

let source = GKRandomSource.sharedRandom()
source.arrayByShufflingObjects(in: arr) // [3, 7, 5, 1, 4, 2, 6]
</code>

with seed
<code>
import GameplayKit

var arr = [1,2,3,4,5,6,7]

let source = GKLinearCongruentialRandomSource()
source.seed = 12345
source.arrayByShufflingObjects(in: resultsArray)
</code>