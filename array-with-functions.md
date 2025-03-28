# array with functions

_Status: Published_
_Created: 2018-02-08 02:04:02_
_Tags: iOS swift_

<code>
class Bla
{
   let arrayOfFunctions = [function1, function2]

   func function1() 
   {
      print("function1")
   }

    func function2() {
        print("function2")
    }

   func useTheFuncs()
   {
    let fn1 = arrayOfFunctions[0]
    fn1(self)()
   }
}
</code>