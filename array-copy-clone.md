# Array copy clone

_Status: Published_
_Created: 2017-12-14 03:25:13_
_Tags: swift_

<code>
//Protocal that copyable class should conform
protocol Copying {
    init(original: Self)
}

//Concrete class extension
extension Copying {
    func copy() -> Self {
        return Self.init(original: self)
    }
}

//Array extension for elements conforms the Copying protocol
extension Array where Element: Copying {
    func clone() -> Array {
        var copiedArray = Array<Element>()
        for element in self {
            copiedArray.append(element.copy())
        }
        return copiedArray
    }
}

//Simple Swift class that uses the Copying protocol
final class MyClass: Copying {
    let id: Int
    let name: String
    
    init(id: Int, name: String) {
        self.id = id
        self.name = name
    }
    
    required init(original: MyClass) {
        id = original.id
        name = original.name
    }
}

//Array cloning
let objects = [MyClass]()
//fill objects array with elements
let clonedObjects = objects.clone()
</code>