# Remove Duplicates Use a Set

_Status: Published_
_Created: 2016-10-12 03:11:21_
_Tags: swift_

<code>
// Initialize the Array
var a = [1,2,3,4,5,2,4,1,4,3,6,5]

// Remove duplicates:
// first by converting to a Set
// and then back to Array
a = Array(Set(a))

print(a)
</code>