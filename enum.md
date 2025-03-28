# enum

_Status: Published_
_Created: 2015-02-07 03:49:05_
_Tags: swift_

<code>
enum Shape {
    case Dot
    case Circle(radius: Double) // Require argument name!
    case Square(Double)
    case Rectangle(width: Double, height: Double) // Require argument names!
    func area() -> Double {
        switch self {
        case Dot:
            return 0
        case Circle(let r): // Assign the associated value to the constant 'r'
            return 3.14*r*r
        case Square(let l):
            return l*l
        case Rectangle(let w, let h):
            return w*h
        }
    }
}
var shape = Shape.Circle(radius: 3.0)
shape.area()//28.26
shape = Shape.Dot
shape.area()//0.0
shape = .Square(2)
shape.area()//4.0
shape = .Rectangle(width: 3, height: 4) // Argument names required
shape.area()//12.0
</code>