# Random In

_Status: Published_
_Created: 2016-06-14 08:05:52_
_Tags: swift_

<code>
func randomNumberIn(range:Range<Int>)->Int
{
    let result = 0
    let random = range.minElement()!  + Int(arc4random_uniform(UInt32((range.maxElement()!+1) - range.minElement()!)))
    if random != 0
    {
        return random
    }
    return result
}
</code>
bv:
<code>
let r = randomNumberIn(0...255)
let g = randomNumberIn(0...255)
let b = randomNumberIn(0...255)
backgroundColor = UIColor(red: r, green: g, blue: b)
</code>

gameplaykit
<code>
let source = GKPerlinNoiseSource(
frequency:2,
octave:3,
persistance: 0.5,
lacunarity: 2
)
let noise = GKNoise(source)
</code>