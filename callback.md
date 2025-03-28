# callback

_Status: Published_
_Created: 2015-02-07 03:50:26_
_Tags: swift_

<code>
class CallbackTest {
    var i = 5
    var callback: (Int -> ())? // NOTE: The optional callback takes an Int
    deinit { // NOTE: This is like -dealloc in Objective-C
        println("Deinit")
    }
}

var obj = CallbackTest()
obj.callback = {
    [unowned obj] // NOTE: Without this, deinit() would never be invoked!
    a in
    obj.i = a
}
</code>