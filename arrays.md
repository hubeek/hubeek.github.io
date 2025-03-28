# Arrays

_Status: Published_
_Created: 2020-10-06 13:45:13_
_Tags: javascript_

Declare Array
let products = [];
let todos = new Array();
The recommended way is to use [] notation to create arrays.

Merge Two Arrays by concat() method
let array1 = [1,2,3];
let array2 = [4,5,6];
let merged = array1.concat(array2);
console.log(merged);
// expected output: Array [1,2,3,4,5,6]
The concat() method is used to merge two or more arrays. This method returns a new array instead to changing the existing arrays.

ES6 Ways to merge two array
let array1 = [1,2,3];
let array2 = [4,5,6];
let merged = [...array1, ...array2];
console.log(merged);
// expected output: Array [1,2,3,4,5,6]
Get the length of Array
To get the length of array or count of elements in the array we can use the length property.

let product = [1,2,3];
product.length // returns 3
Adding items to the end of an array
Let us add some items to the end of an array. We use the push() method to do so.

let product = ['apple', 'mango'];
product.push('banana');
console.log(projects); 
// ['apple', 'mango', 'banana']
Adding items to the beginning of an array
let product = ['apple', 'mango'];
product.unshift('banana');
console.log(projects); 
// ['banana', 'apple', 'mango']
Adding items to the beginning of an array in ES6
let product = ['apple', 'mango'];
product = ['banana', ...product];
console.log(projects); 
// ['banana', 'apple', 'mango']
Adding items to the end of an array ES6
let product = ['apple', 'mango'];
product = [...product, 'banana'];
console.log(projects); 
// ['apple', 'mango', 'banana']
Remove first item from the array
The shift() method removes the first element from an array and returns that removed element. This method changes the length of the array. It returns undefined if the array is empty.

let product = ['apple', 'mango', 'banana'];
let firstValue= product.shift();
console.log(firstValue); // ['mango', 'banana'];
console.log(firstValue); // apple
Remove portion of an array
JavaScript give us slice method to cut the array from any position. The slice() method returns a shallow copy of a portion of an array into a new array object selected from begin to end (end not included). The original array will not be modified.

arr.slice([begin[, end]])
Example
var elements = ['Task 1', 'Task 2', 'Task 3', 'Task 4', 'Task 5'];

elements.slice(2) //["Task 3", "Task 4", "Task 5"]
elements.slice(2,4)  // ["Task 3", "Task 4"]
elements.slice(1,5) // ["Task 2", "Task 3", "Task 4", "Task 5"]
Remove /adding portion of an array -> splice() method
The splice() method changes the contents of an array by removing existing elements and/or adding new elements. Be careful, splice() method mutates the array.

A detailed reference here at MDN splice method.

array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
Parameters
startIndex at which to start changing the array (with origin 0).

deleteCount (Optional)An integer indicating the number of old array elements to remove.

item1, item2, ... (Optional)The elements to add to the array, beginning at the start index. If you don’t specify any elements, splice() will only remove elements from the array.

Return value
An array containing the deleted elements. If only one element is removed, an array of one element is returned. If no elements are removed, an empty array is returned.

var months = ['Jan', 'March', 'April', 'June'];months.splice(1, 0, 'Feb');
// inserts at 1st index positionconsole.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'June']months.splice(4, 1, 'May');
// replaces 1 element at 4th indexconsole.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'May']
Remove last item from the array -> pop() method
The pop() method removes the last element from an array and returns that element. This method changes the length of the array.

var elements = ['Task 1', 'Task 2', 'Task 3'];
elements.pop() // 'Task 3'
console.log(elements) //  ['Task 1', 'Task 2']; 
Joining arrays -> Join () method
The join() method joins all elements of an array (or an array-like object) into a string and returns this string. This is a very useful method.

var elements = ['Task 1', 'Task 2', 'Task 3'];console.log(elements.join());
// expected output: Task 1,Task 2,Task 3console.log(elements.join(''));
// expected output: Task 1Task 2Task3console.log(elements.join('-'));
// expected output: Task 1-Task 2-Task 3
Looping through array
There are various ways to loop through an array. Let’s see the simple example first.

Looping through array — forEach Loop
The forEach loop takes a function, a normal or arrow and gives access to the individual element as a parameter to the function. It takes two parameters, the first is the array element and the second is the index.

let products = ['apple', 'mango'];
products.forEach((e) => {
  console.log(e);
});
// Output
// apple
// mango
let products = ['apple', 'mango']; 
 products.forEach(function (e) {
  console.log(e);
});
 // Output
// apple
// mango 
Let’s see how we can access the index in forEach. Below I am using the arrow function notation, but will work for es5 function type as well.

 products .forEach((e, index) => {
  console.log(e, index);
});

// Output
// apple 0
// mango 1
Finding Elements in an array — find method
The find() method returns the value of the first element in the array that satisfies the provided testing function. Otherwise undefined is returned.

The syntax is given below.

callback — Function to execute on each value in the array, taking three arguments
***** element — The current element being processed in the array
***** index (optional) — The index of the current element
***** array (optional) — The array find was called upon.
thisArg (optional) — Object to use as this when executing callback.
Return value
A value in the array if any element passes the test; otherwise, undefined.

arr.find(callback[, thisArg])var data = [51, 12, 8, 130, 44];var found = data.find(function(element) {
  return element > 10;
});console.log(found);  // expected output: 51
Looping through an array — for in Loop
A for...in loop only iterates over enumerable properties and since arrays are enumerable it works with arrays.

The loop will iterate over all enumerable properties of the object itself and those the object inherits from its constructor’s prototype (properties closer to the object in the prototype chain override prototypes’ properties).

More reading at MDN for in loop

let products = ['apple', 'mango'];
for(let index in  products) {
   console.log(projects[index]);
}

// Output
// apple
// mango  
Note in the above code, a new index variable is created every time in the loop.

Looping through array — map function ()
The map() function allows us to transform the array into a new object and returns a new array based on the provided function.

It is a very powerful method in the hands of the JavaScript developer.

NOTE: Map always returns the same number of output, but it can modify the type of output. For example, if the array contains 5 element map will always return 5 transformed element as the output.

let num = [1,2,3,4,5];
let squared = num.map((value, index, origArr) => {
   return value * value;
});
The function passed to map can take three parameters.

squared — the new array that is returned
num — the array to run the map function on
value — the current value being processed
index — the current index of the value being processed
origArr — the original array
Map () — Example 1 — Simple
let num = [1,2,3,4,5];let squared = num.map((e) => {
   return e * e;
});
console.log(squared); // [1, 4, 9, 16, 25]
In the above code, we loop through all elements in the array and create a new array with the square of the original element in the array.

A quick peek into the output.

Map () — Example 2— Simple Transformation
Let us take an input object literal and transform it into key-value pair.

For example, let’s take the below array

let projects = ['Learn Spanish', 'Learn Go', 'Code more'];
and transform into key-value pair as shown below.

{
  0:  "Learn Spanish",
  1:  "Learn Go",
  2:  "Code more"
}
Here is the code for the above transformation with the output.

let newProjects = projects.map((project, index) => {
   return {
     [index]: project
   }
});
console.log(newProjects); //  [{0: "apple"}, {1: "mango"},] 
Map () — Example 3 — Return a subset of data
Lets take the below input

let tasks = [
   { "name": "Learn Angular",
     "votes": [3,4,5,3]
   },
   { "name": "Learn React",
     "votes": [4,4,5,3]
   },
];
The output that we need is just the name of the tasks. Let’s look at the implementation

let taskTitles = tasks.map((task, index, origArray) => {
   return {
     name: task.name
   }
});

console.log(taskTitles); //
Looping through an array — filter function ()
Filter returns a subset of an array. It is useful for scenarios where you need to find records in a collection of records. The callback function to filter must return true or false. Return true includes the record in the new array and returning false excludes the record from the new array.

It gives a new array back.

Let’s consider the below array as an input.

let tasks = [
   { "name": "Learn Angular",
     "rating": 3
   },
   { "name": "Learn React",
     "rating": 5
   },
   { "name": "Learn Erlang",
     "rating": 3
   },
   { "name": "Learn Go",
     "rating": 5
   },];
Now lets use the filter function to find all tasks with a rating of 5.

Let’s peek into the code and the result.

let products = [
  {
      "name" : "product 1",
      "rating" : 5
  },
  {
      "name" : "product 2",
      "rating" : 4
  },
  {
      "name" : "product 3",
      "rating" : 5
  },
  {
      "name" : "product 4",
      "rating" : 2
  } 
];
let filteredProducts =  products.filter((product) => {
    return  product.rating === 5;
});
console.log( filteredProducts ); 
// [{"name" : "product 1","rating" : 5},{"name" : "product 3", "rating" : 5}]
Since we are only using one statement in the filter function we can shorten the above function as shown below.

tasks.filter(task => task.rating === 5);
NOTE: Filter function cannot transform the output into a new array.

Looping through an array — reduce function ()
Reduce function loops through array and can result a reduced set. It is a very powerful function, I guess, more powerful than any other array methods (though every method has its role).

From MDN, The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.


Reduce — Simple Example — 1
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer)); // expected output: 10// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
Note: The first time the callback is called, accumulator and currentValue can be one of two values. If initialValue is provided in the call to reduce(), 

then accumulator will be equal to initialValue, and currentValue will be equal to the first value in the array. If no initialValue is provided, then accumulator will be equal to the first value in the array, and currentValue will be equal to the second.

The reason reduce is very powerful is because just with reduce() we can implement our own, map(), find() and filter() methods.

Using reduce to categorize data
Assume you have the below data structure which you would like to categorize into male and female dataset.

let data = [
  {name: "Raphel", gender: "male"},
  {name: "Tom", gender: "male"},
  {name: "Jerry", gender: "male"},
  {name: "Dorry", gender: "female"},
  {name: "Suzie", gender: "female"},
  {name: "Dianna", gender: "female"},
  {name: "Prem", gender: "male"},
];
And we would like the output to be as below

{"female" : [
    {name: "Dorry", gender:"female"},
    {name: "Suzie", gender: "female"},
    {name: "Dianna", gender: "female"},
 ],
 "male" : [
    {name: "Raphel", gender:"male"},
    {name: "Tom", gender:"male"},
    {name: "Jerry", gender:"male"},
    {name: "Prem", gender:"male"},
 ]
}
So, lets get to the code and understand how to achieve the above categorization.

let genderwise = data.reduce((acc,item, index) => {
  acc[item.gender].push(item);
  return acc;    
}, {male: [], female:[]});console.log(genderwise);
The important point above is the reduce function can be initialized with any type of starting accumulator, in the above case an object literal containing

{ male: [], female: []}
I hope this is sufficient to demonstrate the power of reduce method.

Using reduce to implement custom map() function
function map(arr, fn) {
  return arr.reduce((acc, item) => [...acc, fn(item)], []);
}
The above is the implementation of custom map function. In the above function we are passing empty array [] as the initial value for the accumulator and the reduce function is returning a new array with the values from the accumulator spread out and appending the result of invoking the callback function with the current item.

Using reduce to implement custom filter() function
Let’s implement the filter() method using reduce().

function filter (arr, fn) {
  return arr.reduce(function (acc, item, index) {
    if (fn(item, index)) {
      acc.push(item);
    }
    return acc;
  },[]);
}
Let’s see the usage and the output below. I could have overwritten the original Array.prototype.filter, but am doing so to avoid manipulating built-in methods.

Using reduce to implement custom forEach function
Let us know implement our own forEach function.

function forEach(arr, fn) {
  arr.reduce((acc, item, index) => {
    item = fn(item, index);
  }, []);
}
The implementation is very simple compared to other methods. We just grab the passed in array and invoke the reduce, and return the current item as a result of invoking the callback with the current item and index.

Using reduce to implement custom pipe() function
A pipe function sequentially executes a chain of functions from left to right. The output of one function serves as the input to the next function in the chain.

Implementation of pipe function

function pipe(...fns) {
  // This parameters to inner functions 
  return function (...x) { 
    return fns.reduce((v, f) => {
      let result = f(v);
      return Array.isArray(result) ? result: [result];
     },x)
   }
}
Usage
const print = (msg) => {
 console.log(msg);
 return msg;
}
const squareAll = (args) => {
   let result = args.map((a) => {
     return a * a;
   });
   return result;
}
const cubeAll = (args) => {
   let result = args.map((a) => {
     return a * a * a;
   });
   return result;
}
pipe(squareAll,cubeAll, print)(1,2,3); // outputs => [1, 64, 729]

Holes in arrays
Holes in arrays means there are empty elements within the array. This may be because of couples of operations like delete or other operations that left these holes accidentally.

Now having ‘holes’ in an array is not good from a performance perspective. Let us take an example below.

let num = [1,2,3,4,5];  // No holes or gapsdelete num[2];  // Creates holesconsole.log (num);  [1, 2, empty, 4, 5]
So, do not use delete method on array, unless you know what you are doing. delete method doesn’t alter the length of the array.

You can avoid holes in an array by using the array methods splice(), pop() or shift() as applicable.

Changing array length and holes
You can quickly change the length of the array as below.

let num = [1,2,3,4,5];  // length = 5;
num.length = 3; // change length to 3//The below logs outputs
// [1,2,3] -> The last two elements are deleted
console.log(num);
Now, increasing the length this way creates holes.

let num = [1,2,3,4,5];num.length = 10;  // increase the length to 10
console.log(num);  // [1, 2, 3, empty × 10]
Quickly Fill Arrays
Let’s take a look at how to quickly fill or initialize an array.

The Array.prototype.fill() method
The fill method (modifies) all the elements of an array from a start index (default zero) to an end index (default array length) with a static value. It returns the modified array.

Description
The fill method takes up to three arguments value, start and end. The start and endarguments are optional with default values of 0 and the length of the this object.

If start is negative, it is treated as length+start where length is the length of the array. If end is negative, it is treated as length+end.

fill is intentionally generic, it does not require that its this value be an Array object.

fill is a mutable method, it will change this object itself, and return it, not just return a copy of it.

When fill gets passed an object, it will copy the reference and fill the array with references to that object.

Example 1 — Simple fill
new Array(5).fill(“hi”)
//Output => (5) [“hi”, “hi”, “hi”, “hi”, “hi”]
Example 2 — Fill with object
new Array(5).fill({'message':'good morning'})
// Output
// [{message: "good morning"}, {message: "good morning"} , {message: "good morning"}  , {message: "good morning"}  , {message: "good morning"}]
Example 3 — Generate sequence
Array(5).fill().map((v,i)=>i);
The output will be

[0,1,2,3,4,5]
Example 4— More examples
[1, 2, 3].fill(4);               // [4, 4, 4]
[1, 2, 3].fill(4, 1);            // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2);         // [1, 4, 3]
[1, 2, 3].fill(4, 1, 1);         // [1, 2, 3]
[1, 2, 3].fill(4, 3, 3);         // [1, 2, 3]
[1, 2, 3].fill(4, -3, -2);       // [4, 2, 3]
[1, 2, 3].fill(4, NaN, NaN);     // [1, 2, 3]
[1, 2, 3].fill(4, 3, 5);         // [1, 2, 3]
Array(3).fill(4);                // [4, 4, 4]
The Array.from method (static method)
The Array.from() function is an inbuilt function in JavaScript which creates a new array instance from a given array. In case of a string, every alphabet of the string is converted to an element of the new array instance and in case of integer values, new array instance simple take the elements of the given array.

Syntax

Array.from(object, mapFunction, thisValue)
Example 1 — Simple example
console.log(Array.from('foo'));
The output will be

["f", "o", "o"]
Example 2 — Object length
Array.from({ length: 5 });
The output will be

[undefined, undefined, undefined, undefined, undefined]