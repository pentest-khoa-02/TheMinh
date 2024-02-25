# What is ES6?
* ES6 (also known as ECMAScript 2015 or ECMAScript 6) is the newer version of JavaScript that was introduced in 2015 and major edition of the ECMAScript language specification standard.
* ECMAScript is the standard that JavaScript programming language uses. ECMAScript provides the specification on how JavaScript programming language should work.
### Top 10 features of ES6: Block-Scoped Constructs Let and Const, Arrow Functions, Multi-line Strings, Default Parameters, Template Literals, Destructuring Assignment, Enhanced Object Literals, Promises, Classes, Modules.
### 1. Block-Scoped Constructs Let and Const
* Before ES6 (2015), JavaScript variables had only Global Scope and Function Scope.
* ES6 introduces two new keywords, let and const, to declare variables. Both of them declare block-scoped variables i.e., the variable is only accessible in the block it is defined.
* Variables declared inside a { } block cannot be accessed from outside the block.
* Let is used to declare block-scoped variables that can be mutated i.e., reassigned.
* Const is used to declare block-scoped variables that cannot be mutated. It points to the same data or object and cannot be changed.
```javascript
{
    let a = 0;
    a = 666;
    {
        const b = 0;
        b = 888; // error
        console.log("a =", a);
        // Output: a = 666
    }
    console.log("b =", b); // error
}

{
    var x = 0;
    x = 666;
    {
        var y = 888;
        y = 888;
        console.log("x =", x);
        // Output: x = 666
    }
    console.log("y =", y); // Output: y = 888
}
```

### 2. Arrow Functions
* ES6 provides a feature known as Arrow Functions. It provides a more concise syntax for writing function expressions by removing the "function" and "return" keywords.
* Arrow functions are defined using the fat arrow (=>) notation.
```javascript
let a = 1;
let b = 99;
// Regular Javascript Function
function sum(a, b){
    console.log("sum:",a + b);
}
// Output: sum: 100
sum(a,b);

// Arrow Function
const mul = (a, b) => {
    console.log("mul:",a * b);
}
mul(a,b);
// Output mul: 99
```

### 3. Multi-line Strings
* ES6 also provides Multi-line Strings. Users can create multi-line strings by using back-ticks(`).
```javascript
let kk = `Hello,
My name is Minh,
Goodbye =))`
console.log(kk);
// Output: Hello,
// My name is Minh,
// Goodbye =))
```

### 4. Default Parameters
* Default Parameters are parameters that are given as default values while declaring a function. It allows getting a default value if the argument is not passed to the function.
```javascript
const r = (x, y = 2) => x ** y;
console.log("3 ^ 2:",r(3));
console.log("3 ^ 2:",r(3,3));
// Output: 3 ^ 2: 9
//        3 ^ 2: 27
```

### 5. Template Literals
* ES6 introduces very simple string templates along with placeholders for the variables. Template literals allow you to embed any variable or expression inside a string.
```javascript
const firstname = 'Minh';
const lastname = 'Nguyen The';

// Old way
console.log('Hi ' + firstname + ' ' + lastname + '!');
// Output: Hi Minh Nguyen The!

// Using template literals
console.log(`Hi ${firstname} ${lastname}!`);
// Output: Hi Minh Nguyen The!
```

### 6. Destructuring Assignment
* Destructuring is one of the most popular features of ES6. The destructuring assignment is an expression that makes it easy to extract values from arrays, or properties from objects, into distinct variables.
* There are two types of destructuring assignment expressions, namely, Array Destructuring and Object Destructuring. It can be used in the following manner
```javascript
//Array Destructuring
let fruits = ["Apple", "Pineapple"];
let [x, y] = fruits; // Array destructuring assignment
console.log(x, y);
// Output: Apple Pineapple

//Object Destructuring
let person = {name: "Minh", age: 66};
let {name, age} = person; // Object destructuring assignment
console.log(name, age);
// Output: Minh 66
```

### 7. Enhanced Object Literals
* ES6 provides enhanced object literals which make it easy to quickly create objects with properties inside the curly braces.
```javascript
function getMobile(manufacturer, model, year) {
    return {manufacturer, model, year}}   
console.log(getMobile("Huawei", "Mate", "99 Vjp Pro"));
// Output: { manufacturer: 'Huawei', model: 'Mate', year: '99 Vjp Pro' }
```

### 8. Promises
* ES6 introduces a new feature called Promises to deal with asynchronous code and save us from callback hell. It can be used to perform async tasks like fetching data from an API. You can also create your own promises and use them elsewhere in the code. Promises either resolve i.e., returns data, or reject i.e., returns an error.
* Simply said a promise is a function that returns an Object to which callbacks can be attached.
* Only when the operation is finished will a promise object's callbacks be activated. Callbacks must wait till the procedure is finished or declined.
* A promise must pass through several phases before it settles (it either is fulfilled or is rejected):

| STATE     | DESCRIPTION                                                                          | CALLBACK   |
| --------- | ------------------------------------------------------------------------------------ | ---------- |
| pending   | Means that the procedure is ongoing and the promise is not yet fulfilled.            | \-         |
| fulfilled | The procedure was finished and was successful.                                       | .then()    |
| rejected  | Even though the procedure was successful, there was a mistake.                       | .catch()   |
| settled   | This callback is triggered whenever the promise has either been resolved or refused. | .finally() |

* A promise's initial state when it is established is pending. The promise is then either fulfilled or denied based on the operation's outcome.
```javascript
// Promise
let m = 0;
let a = new Promise(function(resolve, reject){
    resolve(1);
    //reject(1);
});
a.then(function(value){
    m = value;
    console.log(m);
}).then(function(){
    m = 2;
    console.log(m);
}).then(function(){
    m = 3;
    console.log(m);
    abc,xyz(113);1
}).then(function(){
    m = 4;
    console.log(m);
}).catch(function(){
    m = 5;
    console.log(m);
}).then(function(){
    m = 6;
    console.log(m);
}).finally(function(){
    m = 999;
    console.log(m);
})
// If the promise is kept {resolve(1)} then Output is "1 2 3 5 6 999" else {reject(1)} is "5 6 999"
```

### 9. Classes
* Classes are the core of OOP (Object Oriented Programming). Classes are used to make your code more secure and encapsulated. Classes in ES6 are just syntactic sugar over the conventional functional inheritance system using prototypes that developers are used to. But it also introduces powerful features like constructors, private fields, extend keywords which make it feel like you are working with an object-oriented language. This makes Javascript, both a functional as well as an object-oriented language.
```javascript
class Profile{   
    constructor(firstName, lastName) { 
        this.firstName = firstName;
        this.lastName = lastName;     
    }
    getName() {       
        console.log(`The Full-Name is ${this.firstName} ${this.lastName}`);    
    } 
}
let a = new Profile('Minh', 'Nguyen The');
a.getName(); // output: The Full-Name is Minh Nguyen The
```

### 10. Modules
* Previously, there was no native support for modules in JavaScript. ES6 introduced a new feature called modules, in which each module is represented by a separate ".js" file. We can use the "import" or "export" statement in a module to import or export variables, functions, classes or any other component from/to different files and modules.

File modun-ne.js
```javascript
export var year = 2024; 
export function getnextyear(y) {   
   return y + 1;
};
```
File main.js
```javascript
import {year, getnextyear} from './modun-ne.js';
console.log(year, getnextyear(year));
// Output: 2024 2025
```
