# Javascript  

## Statements vs Expressions  
JavaScript distinguishes expressions and statements:     

Example:
```js
// A statement performs an action.
(param1, param2) => { statements }

// An arrow function with curly brackets needs to have the return keyword.
(param1, param2) => { return expression; }

// An expression produces a value and can be written wherever a value is expected, for example as an argument in a function call. 
(param1, param2) => expression

//Arrow functions without parameters need to have brackets to define the function.
() => { statments }
() => expression
() => { return expression; }
```

## Functions  
Simple function declarations:  
```js
function hello() {
	console.log('Hello Javascript!')
}
hello()
```
ES5 vs ES6:
```js
let helloW = function(name) {
   console.log('Hello ' + name)
 }

let helloW = (name) => {
  console.log('Hello ' + name)
}
helloW('Hello World!')
``` 
ES6 combination:  
```js
let sum = (number1, number2) => {
  return number1 + number2
}
console.log(sum(1,2))
=> 3
```
All functions below are using this function greet() originally:
```js
function greet(value, callback) {
  callback(value)
}
```
A callback function:
```js
function cb(val) {
console.log('Hello ' + val)
}
=> Returns the "Hello Jane/Clarissa"
```
Passing a function call to a callback function as an argument (argument, functioncall) to the greet function:
```js
greet('Jane', cb)
```
Or pass in the arrow function directly as an argument, omitting the callback function as a separate function to call greet():
```js
greet('Clarissa', (name) => console.log(`Bonjour ${name}`))
```

## Array.map()  
The [map() method]((https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)) creates a new array with the results of calling a provided function on every element in the calling array.  
```js
let numbers = [1, 2, 3, 4, 5]
```
Different ways to create a function using map():
```js
let doubles = numbers.map(number => {
  return number * 2;
})
console.log(doubles)
=> [ 2, 4, 6, 8, 10 ]
```
```js
let squares = numbers.map(number => number * number)
console.log(squares)
=> [ 1, 4, 9, 16, 25 ]
```

## Array.filter()   
The [filter() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) creates a new array with all elements that pass the test implemented by the provided function.
Different ways to achieve the same result:
```
Basic hash:

let people = [
  {name: 'Raoul', gender: 'male', age: '40'}, 
  {name: 'John', gender: 'male', age: '20'},
  {name: 'Jane Doe', gender: 'female', age: '20'}
]
```
### Example #1
```js
let result = people.filter((person) => {
  if(person.name.length <= 5)
    return person
})
console.log(result);
=> [ { name: 'Raoul', gender: 'male', age: '40' },
  { name: 'John', gender: 'male', age: '20' } ]
```
```js
let result = people.filter((person) => {
    if(person.gender == 'female')
      return person
  })
console.log(result)
=> [ { name: 'Jane Doe', gender: 'female', age: '20' } ]
```
### Example #2
By using a one-liner arrow function we just need to specify the filtering condition and the return values are taken care of:
```js
let resultRefactor = people.filter(person => person.name.length <= 5)

console.log(resultRefactor);
=> [ { name: 'Raoul', gender: 'male', age: '40' },
  { name: 'John', gender: 'male', age: '20' } ]
```
OR Implementation with for-loop using an empty array
```js
let resultForLoop = []
for (var i = 0; i < people.length; i++) {
  if (people[i].name.length <= 5)
    resultForLoop.push(people[i])
}

console.log(resultForLoop)
=> [ { name: 'Raoul', gender: 'male', age: '40' },
  { name: 'John', gender: 'male', age: '20' } ]
```
## Destructuring  
Destructuring is a new feature in ES6 where we are given the ability to extract data from object and arrays and set them with new variables.

### Example #1:  
Let's assume the following array:
```js
let persons = ['Jane', 'raoul', 'bob']

//Before ES6
console.log(persons[0])

//With ES6
let [ jane, tom, name3 ] = persons

console.log(tom)
=> 'raoul'

console.log(name3)
=> 'bob'
```
i.e. the values jane, tom, name3 become new placeholders for the original values in the persons array.
Other ways of accessing the values of the __persons__ array:
```js
let [name1, ...rest] = persons
console.log(name1)
//returns Jane
console.log(rest)
//returns all values except for the first one.
```
### Example #2:
Object Matching:
```js
let people = [
    {name: 'Raoul', gender: 'male', age: '40'}, 
    {name: 'Jane', gender: 'female', age: '20'}
  ]
  
  // Before destructuring
  people.forEach((person) => {
    console.log(`Hi, my name is ${person.name}, I am a ${person.age} year old`)
  })
  
  // With destructuring
  // key1, key2
  people.forEach(({ name, age }) => {
    console.log(`Hi, my name is ${name}, I am a ${age} year old`)
  })
 
  // Renaming with destructing
  // Assigning new keys to the original keys
  people.forEach(({ name: b, age: a }) => {
    console.log(`Hi, my name is ${b}, I am a ${a} year old`)
  })
```
More examples of object desctructuring:
```js
const raoul = {
    name: 'Raoul Diffouo',
    role: 'Software Engineer',
    social: {
      github: 'https://github.com/diraulo',
      twitter: 'https://twitter.com/diraulo'
    }
  }
  
  // to get the social links you'd do something like
  let github = raoul.social.github
  let twitter = raoul.social.twitter

  // OR you could just do the following:
  
  let { github, twitter } = raoul.social
  
  console.log(github)
  console.log(twitter)
  
  // OR Renane when destructuring; produces exact same result
  
  let { github: gh, twitter: tweet } = raoul.social
  console.log(gh)
  console.log(tweet)
  ```

## Loops  
Using the following array:
```js
let people = [
  {name: 'Raoul', gender: 'male', age: '40'}, 
  {name: 'John', gender: 'male', age: '20'}
]
```
All of the code examples below will produce the exact same output:
```js
//A regular foor loop to call each name for the string
for (var i = 0; i < people.length; i++) {
  console.log(`Hello, ${people[i].name}`)
}

// in Ruby
// people.each do |person|
//   puts "Hello, #{person.name}"
// end

//Same as Ruby's .each mapping method for string interpolation
people.forEach(function(person) {
  console.log(`Hello, ${person.name}`)
})

//As an arrow function.
people.forEach((person) => {
  console.log(`Hello, ${person.name}`)
})

// Can also be writen as follows
people.forEach(person => console.log(`Hello, ${person.name}`))
```

## [Classes](https://www.digitalocean.com/community/tutorials/understanding-classes-in-javascript) (ES6) vs [Constructor functions](https://www.digitalocean.com/community/tutorials/understanding-prototypes-and-inheritance-in-javascript) (ES5) 

Although you may see similarities between class and object syntax, there is one important method that sets them apart: the constructor method. JavaScript will invoke the constructor() method every time we create a new instance of our class.  
```js
class Person { 
    constructor(first, last) {
      this.first = first;        
      this.last = last;
    }
}  
```
Inside of the constructor() method, we use the __this__ keyword. In the context of a class, this refers to an instance of that class. An instance is an object that contains the property names and methods of a class but with unique property values. 

Inside of the constructor() method, we use the __this__ keyword. In the context of a class, __this__ refers to an instance of that class. In the Person class, we use this to set the value of the Person's instance’s first property to the first argument. In this case the value is equal to the input parameter, however, it could also have been set to always be initialized to something for every instance of the Person class like the name 'Jane'.  

```js
class Person { 
    constructor(first, last) {
      this.first = first;        
      this.last = last;
    }
}  
  
const bob = new Person("Bob", "The Builder")
```
We can use the __new__ keyword to create an instance of our Person class. The keyword calls the constructor(), runs the code inside of it, and then returns the new instance. Here, we have created a new variable called 'bob' that will store an instance of our Person class. 

When we pass the two arguemnts as strings "Bob" and "The Builder" to the Person constructor, it sets/saves the __first__ and __last__ property to 'Bob' and 'The Builder'. 

### Getter and setter  
We can add getters and a method to bring our class to life.
Class method and getter syntax is the same as it is for objects except you cannot include commas between methods.

```js
class Person { 
  constructor (first, last) {
    this.first = first;        
    this.last = last;
  }

  get fullName() {
    return `${this.first} ${this.last}`
  }

}

const bob = new Person("Bob", "The Builder")
```


// ```js
// function Person(first, last) { 
//     // create "constructor"
//     this.first = first;        
//     // public variables -- reference current object
//     this.last = last;

//     this.setName = function(first, last){ 
//         // public function
//         this.first = first;
//         this.last = last;
//     }
// }

// Person.prototype.fullName = function() { 
//     // extend prototype
//     return this.first + ' ' + this.last; 
//     // even at runtime!
// }

// var bob = new Person("My", "Person"); 
// // "new" creates an object
// bob.fullName();               
// // "My Person"

// //ES6

// class Person { 
//     constructor(first, last) {
//       this.first = first;        
//       this.last = last;
//     }
  
//   get fullName() { 
//     return this.extraMethod()
//     }   
//     extraMethod() {
//       return `${this.first + " " + this.last}`
//     }
//   }
  
//   const bob = new Person("New", "Person")
//   bob.fullName

// ```
// Create a superclass of another class:  
// ```js
// class Person { 
//   constructor (first, last) {
//     this.first = first;        
//     this.last = last;
//   }

//   get fullName() {
//     return `${this.first} ${this.last}`
//   }

// }

//   class Woman extends Person {
//     constructor(first, last) {
//       super(first, last)
//     }
//   }

// const bob = new Person("Bob", "The Builder")
// const edna = new Woman("Edna", "Krabapel")

// bob.fullName + edna.fullName 
// ````

## JavaScript vs jQuery  
### What is jQuery?  
- not a programming language, but rather an elegant lower-level API (used to be a popular programming language for many years) to make working with the DOM easier across browsers.  
- created to condense common JS tasks into fewer lines of code. Most of the common JS tasks can be coded using jQuery (related to UI). 
- easy to install and understand (more user friendly interface).  
- found in many legacy projects.  

builtwith.com  

- Everything you can do in jQuery can be done in JS and vice versa. 
**Example difference:**
```js
document.getElementbyClassName("simple-li");
vs
$('.simple-li')
```
Hide and show (JQ vs JS):
```js
$(el).hide();
== el.style.display = 'none';
OR
$(el).show();
== el.style.display = '';
```
Add a class to an element
```js
$(el).addClass(className);
==
if (el.classList)
  el.classList.add(className);
else
  (el.className += ' ' + className);
```
Add content/text to an element:
```js
$(el).after(htmlString);
==
el.insertAdjacentHTML('afterend', htmlString)

$(parent).append(el);
==
parent.appendChild(el)
```
Remove conent/text:
```js
$(el).empty();
==
el.innerHTML = '';
```
Is Page Loaded?  
```js
$(document).ready(function()){
  //code goes here
});
document.addEventListener('DOMContentLoaded', () => {
  //code goes here
});
```
### Do I have to learn jQuery or are other libraries enough?  
- 'Probably', it is a huge framework however jQuery is rarely mentioned in job listings.  
- There is a learning advantage to learn JS before learning easier frameworks and using the libraries.  
- Foundation/Bootstrap are CSS frameworks, just like to TailWind or Semantic UI.  
- Bootstrap is fully dependent on jQuery.  