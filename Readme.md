
# 1- var, let and const:

## var   : 
Global Scope & can be redeclared And mutable
```js
var j = 0;
var j = 9; // No Error (can be redeclared)
j = 10; // No Error (can be reassigned)

var person = {
  name: 'Nick'
};
person.name = 'John' // this will work 
console.log(person.name) // "John"
```
## let   : 
Block Level Scope & Can't be redeclared but can be reassigned
```js
let j = 0;
let j = 9; // Error (redeclared)
j = 10; // No Error (can be reassigned)

let person = {
  name: 'Nick'
};
person.name = 'John' // this will work 
console.log(person.name) // "John"
```
## const : 
Block Level Scope & Can't be reassigned & Can't be redeclared And mutable
```js
const j = 0;
const j = 9; // Error (redeclared)
j = 10; // Error (reassigned)

const person = {
  name: 'Nick'
};
person.name = 'John' // this will work ! person variable is not completely reassigned, but mutated
console.log(person.name) // "John"
person = "Sandra" // raises an error, because reassignment is not allowed with const declared variables
```

# 2- Hoisting:
Variables and function declarations are moved to the top of their scope before code execution.

## var, let, and const

### var:
Hoisted — declared and initialized with `undefined`.

### let / const:
Hoisted — declared but **not initialized** (they are in the Temporal Dead Zone until their declaration is evaluated).

# 3- Arrow Function
The ES6 JavaScript update has introduced arrow functions, which is another way to declare and use functions. Here are the benefits they bring:

1- More concise (mainly used for single line code)<br />
2- **this** is picked up from surroundings <br />
3- implicit return<br />


## 1- More Concise
```js 
function double(x){
    return 2 * x;
}

double = (x) => x*2;
     // Same function written as an arrow function with implicit return
console.log(double(2)) // 4
```

## 2- **this** is picked up from surroundings

An arrow function doesn't create a new this, it grabs it from its surrounding instead.

```js

// Without Arrow Function


class Match{
    function func(){
    this.myVar = 0; 
    // here this is referencing to the crrent object, so here
    //  we are assigning 0 to myVar variable of current object
    //  (object which has called the function func)
    setTimeout(function(){
        this.myVar++; 
        // this is wrong because now *this* is not talking 
        // about current objects (object which has called the 
        // function func) myVar. here *this* is referencing to the global
        //  instance of Match class or undefined if not declared
        })
    }

    function func(){
        this.myVar = 0; 
        // here this is referencing to the crrent object, so here
        //  we are assigning 0 to myVar variable of current object
        //  (object which has called the function func)
        const that = this; 
        // a new *that* is initialized to keep 
        // track of the object which has called
        //  the func function
        setTimeout(function(){
            that.myVar++; 
            // now this line will work fine
        })
    }
}


// With Arrow function
class Match{
    function func(){
    this.myVar = 0; 
    // here this is referencing to the crrent object, so here
    //  we are assigning 0 to myVar variable of current object
    //  (object which has called the function func)
    setTimeout(() => {
        this.myVar++; 
        // now here *this* is referencing to the currect object of Match
        })
    }

    function func(){
        this.myVar = 0; 
        // here this is referencing to the crrent object, so here
        //  we are assigning 0 to myVar variable of current object
        //  (object which has called the function func)
        const that = this; 
        // Now we don't need this thing
        setTimeout(() => {
            that.myVar++; 
            // use of *that* here is an extra thing
        })
    }
}


```

## 3- Implicit return

```js

const student = () => {
    name: "Ahmad", age: 24
}; 
// Object with name and age keys is impicitly returned

const double = (x) => {
    2*x;
}
//  implicitly returns 2*x



```
### How to avoid this implicit return from returning. i don't need it but i want to use arrow function


use { } brakcets

```js 

const func = () => 2;
console.log(func()) // print 2 on console


const funct = () => {2};
console.log(funct()) // print undefined on console

```
# 4- Default Parameter

Default parameter is used only when no parameter is passed or undefined parameter is passed.


```js

function myNewFunc(x=10){
    return x;
}

console.log(myNewFunc()); 
// print 10 on console
console.log(myNewFunc(5));
// print 5 on console
console.log(undefined);
// print 10 on console
console.log(null);
// print null on console

```

# 5- Destructuring of objects

## UseCase number 1

```js

const person = {
    name: "Ahmad",
    age: 25,
    degree: "BSCS"
}

// Without Destructuring

let name = person.name;
let age = person.age;
let degree = person.degree;

// With Destructuring

const {name: personName, age, degree = "BS" } = person;

console.log(personName) // This will print the name of the person
console.log(name) // This will raise a reference erro since the name is only accessible via person i.e person.name and the new variable being created is named as personName not name
console.log(degree) // will print degree of the person it its null or undefined
```

## UseCase Number 2

#### Mainly we use destructuring for passing the content of objects as parameter to the functions

```js

// With Destructuring

function funga({firstName, lastName}){
    return firstName + '-' + lastName;
}

funga(person)

// Without Destructuring

function funga(person){
    let firstName = person.firstName;
    let lastName = person.lastName;
    return firstName + '-' + lastName;
}

funga(person)

```

## UseCase Number 3

#### Destructuring when used with arrow functions, gives its real taste

```js
const funga = ({firstName, lastName}) => ({firstName + '-' + lastName;}
)
// This will return same result as of usecase 2
```

# 6- Functional Programming

### Functional Programming is defined as a paradigm of programming in which we follow four major points:
#### 1- Always make Pure Functions
#### 2- Function Composition used
#### 3- No shared state
#### 4- Original data not Mutable
#### 5- No Side Effects

## 1- Pure Function:
A function which gives same output everytime for same input, and does not change anything outside itslef (globally etc.)
```js
const double = (x) => 2*x;
// a Pure Function
```

## 2- Function Composition
It means you use more than one functions collectively in a row to get final answer.
```js 
const double = (x) => 2*x;
const increment = (x) => x+1;

const result = increment(double(4));
```

## 3- Shared State
Common resource used by multiple processes. If two processes are using same variable, change by one can break the other. FP avoids this by just passing the data.

#### Why dealing with shared state is hard?
Because it results in **Bugs** like **race conditions** and **Timing Problem**

## 4- Original Data not mutable
Never change an existing object
```js
const x = {'val':10};
const y = Object.assign({},x,{'val':x.val+1});
```
## 5- Side Effects
Any action that touches the outside world i.e. API calls

# 7- Higher order Function (HOF):
A function that takes another function as input orr returns one
```js
const double = (x) => 2*x;
[1,2,3].map(double) // returns [2,4,6] 
```

# 8- Modern JS ES6 functions based on Functional Programming

## Arrays methods - map / filter / reduce / find

### map:
Takes an array, does something to its elements and returns a new array with transformed elements

### filter:
takes an array, decides element by element if it should keep it or not and returns an array with kept elements only

### reduce:
takes an array, aggregates its elements into a single value. takes a function and a valueof the accumulator variable

### find:
takes and array, returns the first element that satisfies the provided condition.

#### Example Code:
```js
const number = [0, 1, 2, 3, 4, 5, 6];
const doubleNumbers = numbers.map(x => x*2); // [0,2,4,6,8,10,12]
const evenNumbers = numbers.filter(x%2===0) // [0,2,4,6]
const sum = numbers.reduce((prev,next) => prev + next, 0); // 21 
const greaterThanFour = numbers.find((n)=>n>4); // [5, 6]
```

# 9- Spread Operator and rest operator`...`

to transform a single element place into n elements place. 

```js
const arr1 = [1,2,3];
const arr2 = [...arr1, 4,5,6]; // this is [1,2,3,4,5,6] this is spread operator
const arr3 = [arr1, 4,5,6]; // this is [[1,2,3],4,5,6]

// Similarly

function addition (...parameter){
    return parameter.reduce((sum,number)=>sum+number,0);
}

const mArray = [1,2,3,5]
console.log(addition(...mArray)) // 11

function myFunc(x, y, ...params) // this is rest operator
 {
  console.log(x);
  console.log(y);
  console.log(params)
}

myFunc("a", "b", "c", "d", "e", "f")

```
## UseCase of Rest Operator

let's say we want a function which creates a new student with its grades and with its average grade. Wouldn't it be more convenient to extract the first two parameters into two separate variables, and then have all the grades in an array we can iterate over?

That's exactly what the rest operator allows us to do!

```js
function createStudent(firstName, lastName, ...grades){
  // firstName = "Nick"
  // lastName = "Anderson"
  // [10, 12, 6] -- "..." takes all other parameters passed and creates a "grades" array variable that contains them

    const avgGrades = grades.reduce((sum,num)=>sum+num,0)

    return {
        firstName: firstName,
        lastName: lastName,
        grades: grades,
        avgGrade: avgGrade
    }
    // {
//   firstName: "Nick",
//   lastName: "Anderson",
//   grades: [10, 12, 6],
//   avgGrade: 9,33
// }
}


const newStudent = createStudent("Ahmad","Ali",89,98,78,84);
console.log(newStudent);
```



# 10 - Arguments Object in javascript
*-*
there is a special built-in object called arguments, which is available inside all regular (non-arrow) functions in JavaScript.


```js
function myFunca() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}

myFunca("Nick", "Anderson", 10, 12, 6);

// "a"
// "b"
// ["c", "d", "e", "f"]
```

# 11- Object Properties Spreading

```js
const student = {
    fistName: "Ahmad",
    lastName: "Ali",
    country: "Pakistan",
    city: "Lahore",
    town: "Muhammad Pura",
    street: 3
};

const { firstName, lastName, ...Address } = student;

console.log(firstName); // Ahmad
console.log(lastName); // Ali
console.log(Address); // {country: "Pakistan",
    // city: "Lahore",
    // town: "Muhammad Pura",
    // street: 3}