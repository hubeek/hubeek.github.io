# Random Color with seed

_Status: Published_
_Created: 2018-05-17 16:57:05_
_Tags: iOS swift_

<code>
extension UIColor
{
    func randomColor(seed: String) -> UIColor
    {
        
        var total: Int = 0
        for u in seed.unicodeScalars {
            total += Int(UInt32(u))
        }
        
        srand48(total * 200)
        let r = CGFloat(drand48())
        srand48(total)
        let g = CGFloat(drand48())
        srand48(total / 200)
        let b = CGFloat(drand48())
        
        return UIColor(red: r, green: g, blue: b, alpha: 1)
    }
}

let str = "abcd"
let a = UIColor().randomColor(seed: str)
is the same with
let b = UIColor().randomColor(seed: str)
is the same with
let c = UIColor().randomColor(seed: str)
etc etc
</code>