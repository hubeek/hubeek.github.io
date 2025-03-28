# Looping

_Status: Published_
_Created: 2016-06-14 02:07:06_
_Tags: swift_


<h3>Looping n times</h3>
<code>
for var i = 0; i < 10; i++ {
    print(i)
}
 
// use this: 
for i in 0..<10 {
    print(i)
}
</code>


<h3>Looping n times in reverse</h3>
<code>
for var i = 10; i > 0; i-- {
    print(i)
}
 
// use this
for i in (1...10).reverse() {
    print(i)
}
</code>


<h3>Looping with Stride</h3>
<code>
for var i = 0; i < 10; i += 2 {
    print(i)
}
 
// use this
for i in 0.stride(to: 10, by: 2) {
    print(i)
}
</code>

<h3>Looping through Array Values</h3>
<code>

let someNumbers = [2, 3, 45, 6, 8, 83, 100]
 
// instead of this
for var i = 0; i < someNumbers.count; i++ {
    print(someNumbers[i])
}
 
// use this
for number in someNumbers {
    print(number)
}
 
// or this
someNumbers.forEach { number in
    print(number)
}
</code>


<h3>Reverse Looping through Array Values</h3>
<code>
let someNumbers = [2, 3, 45, 6, 8, 83, 100]
 
/* 100, 83, 8, 6, 45, 3, 2 */
 
// instead of this
for var i = someNumbers.count - 1; i >= 0; i-- {
    print(someNumbers[i])
}
 
// use this
for number in someNumbers.reverse() {
    print(number)
}
</code>



<h3>Looping Through an Array with Index</h3>
<code>
let someNumbers = [2, 3, 45, 6, 8, 83, 100]
 
/*
 1: 2
 2: 3
 3: 45
 4: 6
 5: 8
 6: 83
 7: 100
 */
 
// instead of this
for var i = 0; i < someNumbers.count; i++ {
    print("\(i + 1): \(someNumbers[i])")
}
 
// use this
for (index, number) in someNumbers.enumerate() {
    print("\(index + 1): \(number)")
}
 
// or this
someNumbers.enumerate().forEach { (index, number) in
    print("\(index + 1): \(number)")
}
</code>


<h3>Looping Through Array Indices</h3>
<code>
let someNumbers = [2, 3, 45, 6, 8, 83, 100]
 
/* 0, 1, 2, 3, 4, 5, 6 */
 
// instead of this
for var i = 0; i < someNumbers.count; i++ {
    print(i)
}
 
// use this
for index in someNumbers.indices {
    print(index)
}
</code>



<a href="https://www.natashatherobot.com/swift-alternatives-to-c-style-for-loops/" target="_blank">from: Natasha the Robot </a>