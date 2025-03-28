# remove object from array

_Status: Published_
_Created: 2014-06-06 05:28:59_
_Tags: javascript_

someArray = [{name:"Kristian", lines:"2,5,10"},
             {name:"John", lines:"1,19,26,96"}];
You can use several methods to remove an item from it:

//1
someArray.shift(); // first element removed
//2
someArray = someArray.slice(1); // first element removed
//3
someArray.splice(0,1); // first element removed
//4
someArray.pop(); // last element removed
If you want to remove element at position x, use:

someArray.splice(x,1);