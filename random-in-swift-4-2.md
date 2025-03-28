# Random in swift 4.2

_Status: Published_
_Created: 2018-11-28 06:25:10_
_Tags: iOS swift, 4.2_

<code>
let double = Double.random(in: -1.2...4.5)
let integer = Int.random(in: .min ... .max)
let unsignedInteger = UInt.random(in: 4...9)
let bool = Bool.random() // false/true

struct SeededRandomNumberGenerator: RandomNumberGenerator {
    init(seed: Int) {
        srand48(seed)
    }
    
    func next() -> UInt64 {
        return UInt64(drand48() * Double(UInt64.max))
    }
}

var seededGenerator = SeededRandomNumberGenerator(seed: 5)
var random = Int.random(in: -5...5, using: &seededGenerator) // 2
 random = Int.random(in: -5...5, using: &seededGenerator) // 1
 random = Int.random(in: -5...5, using: &seededGenerator) //-3
 random = Int.random(in: -5...5, using: &seededGenerator) //-2

</code>