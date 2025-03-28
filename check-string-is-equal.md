# check string is equal

_Status: Published_
_Created: 2014-06-06 04:43:23_
_Tags: javascript_

<code>if ( variable.valueOf()=="string" )</code>

"a" == "b"
However, note that string objects will not be equal.

new String("a") == new String("a")
will return false.

Call the valueOf() method to convert it to a primitive for String objects,

new String("a").valueOf() == new String("a").valueOf()