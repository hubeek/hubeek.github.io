# Remove from array

_Status: Published_
_Created: 2015-05-28 02:27:00_
_Tags: swift_

<code>
var array = ["qwe","findmeTORemove","zxc"]

var foundIndex = [Int]()
var ind = 0
for a in array
{
  if a == "findmeTORemove"
  {
    foundIndex.append(ind)
    
  }
  ind++
}
array
for var i = foundIndex.count-1 ; i >= 0 ; i--
{
  array.removeAtIndex(foundIndex[i])
}


array = ["qwe","zxc"]

</code>