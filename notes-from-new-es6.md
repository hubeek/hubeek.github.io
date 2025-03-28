# notes from new es6

_Status: Published_
_Created: 2017-11-24 05:52:40_
_Tags: javascript_

probeer in:
http://jsbin.com/
<hl>
<h2>imports</h2>
You got two different types of exports: default (unnamed) and named exports:

default => export default ...; 

named => export const someData = ...; 

You can import default exports like this:

import someNameOfYourChoice from './path/to/file.js'; 

Named exports have to be imported by their name:

import { someData } from './path/to/file.js'
<h2>snips</h2>
<code>

const myName = 'hjh';
///console.log(myName);

function printName(name){
  console.log(name);
}
const printName2 = (name,age) =>{
  console.log('2: '+name+' age: '+age);
}
//printName("hhhh");
//printName2("hhhh");

const multiply = (number) =>{
  return number * 2;
}
const multiply2 = number => number * 2;

//printName(multiply(4));
//printName(multiply2(4));

class Person{
  
  constructor(name){
    this.name = name;
  }
  
  call() {
    console.log( 'hi from '+ this.name);
  }
}
const p = new Person('hjc');
p.call();

const numbers = [1,2,3];
//spread
const newNumbers = [...numbers,4];
console.log('newNumbers: '+newNumbers);
const newPerson = {
  ...p,
  age: 26
}
console.log(newPerson)

const filter = (...args) => {
  return args.filter(el => el === 1);
}

console.log('filter : '+filter(1,2,3));

[num1,num2] = numbers;
console.log(num1,num2);

// Arrrays & Class's are copied by reference!

const person3 = {
  name: 'Max'
}

const person4 = person3;
const person5 = {
  ...person3
}
person3.name = 'Manu';

console.log(person4);
console.log(person5);

// array .map function
const doubleNumbers = numbers.map((num)=> {return num*2});
console.log('double numbers '+doubleNumbers);
</code>

meer array functions
map()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map
find()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find
findIndex()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex
filter()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter
reduce()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b
concat()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b
slice()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice
splice()  => https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice

react components playground:
https://codepen.io


