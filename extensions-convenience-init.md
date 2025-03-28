# Extensions Convenience init!

_Status: Published_
_Created: 2015-01-10 08:54:00_
_Tags: swift_

<code>extension UIColor{
    
    convenience init(red: Int, green: Int, blue: Int)
    {
        let newRed   = CGFloat(Double(red) / 255.0)
        let newGreen = CGFloat(Double(green) / 255.0)
        let newBlue  = CGFloat(Double(blue) / 255.0)
        
        self.init(red: newRed, green: newGreen, blue: newBlue, alpha: CGFloat(1.0))
    }
}

let swiftOrange = UIColor(red: 255, green: 149, blue: 0)
let swColor = UIColor(red:34, green:223, blue:123)
</code>