# Singleton approach

_Status: Published_
_Created: 2015-07-26 08:44:09_
_Tags: swift_

<code>
class TestSingleton {
  static let sharedInstance = TestSingleton()
  var title = ""
  private init() {}
}

let t1 = TestSingleton.sharedInstance
t1.title = "A"
let t2 = TestSingleton.sharedInstance
t2.title = "B"

println(t1.title) // B
println(t2.title) // B
</code>