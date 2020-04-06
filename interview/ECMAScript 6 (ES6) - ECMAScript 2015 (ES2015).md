# ECMAScript 6 (ES6)/ ECMAScript 2015 (ES2015)

## Could you explain the difference between ES5 and ES6
-   **ECMAScript 5 (ES5)**: The 5th edition of ECMAScript, standardized in 2009. This standard has been implemented fairly completely in all modern browsers
    
-   **ECMAScript 6 (ES6)/ ECMAScript 2015 (ES2015)**: The 6th edition of ECMAScript, standardized in 2015. This standard has been partially implemented in most modern browsers.

Here are some key differences between ES5 and ES6:

-   **Arrow functions**  &  **string interpolation**:  
    Consider:
    
    ```js
    const greetings = (name) => {
        return `hello ${name}`;
    }
    ```
    
    and even:
    
    ```js
    const greetings = name => `hello ${name}`;
    ```
    
-   **Const**.  
    Const works like a constant in other languages in many ways but there are some caveats. Const stands for ‘constant reference’ to a value. So with const, you can actually mutate the properties of an object being referenced by the variable. You just can’t change the reference itself.
    
    ```js
    const NAMES = [];
    NAMES.push("Jim");
    console.log(NAMES.length === 1); // true
    NAMES = ["Steve", "John"]; // error
    ```
    
-   **Block-scoped variables**.  
    The new ES6 keyword  `let`  allows developers to scope variables at the block level.  `Let`  doesn’t hoist in the same way  `var`  does.
    
-   **Default parameter values**  Default parameters allow us to initialize functions with default values. A default is used when an argument is either omitted or undefined — meaning null is a valid value.
    
    ```js
    // Basic syntax
    function multiply (a, b = 2) {
       return a * b;
    }
    multiply(5); // 10
    ```
    
-   ** Class Definition and Inheritance**  
    ES6 introduces language support for classes (`class`  keyword), constructors (`constructor`  keyword), and the  `extend`  keyword for inheritance.
    
-   **for-of operator**  
    The for...of statement creates a loop iterating over iterable objects.
    
-   **Spread Operator**  For objects merging
    
    ```js
    const obj1 = { a: 1, b: 2 }
    const obj2 = { a: 2, c: 3, d: 4}
    const obj3 = {...obj1, ...obj2}
    ```
    
-   **Promises**  
    Promises provide a mechanism to handle the results and errors from asynchronous operations. You can accomplish the same thing with callbacks, but promises provide improved readability via method chaining and succinct error handling.
    
    ```js
    const isGreater = (a, b) => {
    return new Promise ((resolve, reject) => {
      if(a > b) {
        resolve(true)
      } else {
        reject(false)
      }
      })
    }
    isGreater(1, 2)
    .then(result => {
      console.log('greater')
    })
    .catch(result => {
      console.log('smaller')
    })
    ```
    
-   **Modules exporting & importing**  Consider module exporting:
    
    ```js
    const myModule = { x: 1, y: () => { console.log('This is ES5') }}
    export default myModule;
    ```
    
    and importing:
    
    ```js
    import myModule from './myModule';
    ```

## What is IIFEs (Immediately Invoked Function Expressions)?
It’s an Immediately-Invoked Function Expression, or IIFE for short. It executes immediately after it’s created:

```js
(function IIFE(){
    console.log( "Hello!" );
})();
// "Hello!"
```

This pattern is often used when trying to avoid polluting the global namespace, because all the variables used inside the IIFE (like in any other normal function) are not visible outside its scope.

## What are the benefits of using spread syntax in ES6 and how is it different from rest syntax?
ES6's spread syntax is very useful when coding in a functional paradigm as we can easily create copies of arrays or objects without resorting to  `Object.create`,  `slice`, or a library function. This language feature is used often in Redux and rx.js projects.

```js
function putDookieInAnyArray(arr) {
  return [...arr, 'dookie'];
}

const result = putDookieInAnyArray(['I', 'really', "don't", 'like']); // ["I", "really", "don't", "like", "dookie"]

const person = {
  name: 'Todd',
  age: 29,
};

const copyOfTodd = { ...person };
```

ES6's rest syntax offers a shorthand for including an arbitrary number of arguments to be passed to a function. It is like an inverse of the spread syntax, taking data and stuffing it into an array rather than unpacking an array of data, and it works in function arguments, as well as in array and object destructuring assignments.

```js
function addFiveToABunchOfNumbers(...numbers) {
  return numbers.map(x => x + 5);
}

const result = addFiveToABunchOfNumbers(4, 5, 6, 7, 8, 9, 10); // [9, 10, 11, 12, 13, 14, 15]

const [a, b, ...rest] = [1, 2, 3, 4]; // a: 1, b: 2, rest: [3, 4]

const { e, f, ...others } = {
  e: 1,
  f: 2,
  g: 3,
  h: 4,
}; // e: 1, f: 2, others: { g: 3, h: 4 }
```

## What are the differences between ES6 class and ES5 function constructors?
Let's first look at example of each:

```js
// ES5 Function Constructor
function Person(name) {
  this.name = name;
}

// ES6 Class
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

For simple constructors, they look pretty similar.

The main difference in the constructor comes when using inheritance. If we want to create a  `Student`  class that subclasses  `Person`  and add a  `studentId`  field, this is what we have to do in addition to the above.

```js
// ES5 Function Constructor
function Student(name, studentId) {
  // Call constructor of superclass to initialize superclass-derived members.
  Person.call(this, name);

  // Initialize subclass's own members.
  this.studentId = studentId;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

// ES6 Class
class Student extends Person {
  constructor(name, studentId) {
    super(name);
    this.studentId = studentId;
  }
}
```

It's much more verbose to use inheritance in ES5 and the ES6 version is easier to understand and remember.

## Give example of ES6 classes?
```js
// ***ES2015+**
class Person {
    constructor(first, last) {
        this.first = first;
        this.last = last;
    }

    personMethod() {
        // ...
    }
}

class Employee extends Person {
    constructor(first, last, position) {
        super(first, last);
        this.position = position;
    }

    employeeMethod() {
        // ...
    }
}
```

## Explain the difference between Object.freeze() vs const
`const`  and  `Object.freeze`  are two completely different things.

-   `const`  applies to  **bindings**  ("variables"). It creates an immutable binding, i.e. you cannot assign a new value to the binding.
    
    ```js
    const person = {
      name: "Leonardo"
    };
    let animal = {
      species: "snake"
    };
    person = animal; // ERROR "person" is read-only
    ```
    
-   `Object.freeze`  works on  **values**, and more specifically,  _object values_. It makes an object immutable, i.e. you cannot change its properties.
    
    ```js
    let person = {
      name: "Leonardo"
    };
    let animal = {
      species: "snake"
    };
    Object.freeze(person);
    person.name = "Lima"; //TypeError: Cannot assign to read only property 'name' of object
    console.log(person);
    ```

## What is generator in JS?
Generators are functions which can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances. Generator functions are written using the  `function*`  syntax. When called initially, generator functions do not execute any of their code, instead returning a type of iterator called a Generator. When a value is consumed by calling the generator's  `next`  method, the Generator function executes until it encounters the  `yield`  keyword.

The function can be called as many times as desired and returns a new Generator each time, however each Generator may only be iterated once.

```js
function* makeRangeIterator(start = 0, end = Infinity, step = 1) {
    let iterationCount = 0;
    for (let i = start; i < end; i += step) {
        iterationCount++;
        yield i;
    }
    return iterationCount;
}
```

## What is Hoisting in JavaScript?
_Hoisting_  is the JavaScript interpreter's action of moving all variable and function declarations to the top of the current scope. There are two types of  _hoisting_:

-   variable hoisting - rare
-   function hoisting - more common

Wherever a  `var`  (or function declaration) appears inside a scope, that declaration is taken to belong to the entire scope and accessible everywhere throughout.

```js
var a = 2;
foo();                   // works because `foo()`
                         // declaration is "hoisted"

function foo() {
    a = 3;
    console.log( a );    // 3
    var a;               // declaration is "hoisted"
                         // to the top of `foo()`
}

console.log( a );    // 2
```

## What is the Temporal Dead Zone in ES6?
In ES6  `let`  and  `const`  are hoisted (like  `var`,  `class`  and  `function`), but there is a period between entering scope and being declared where they cannot be accessed.  **This period is the temporal dead zone (TDZ)**.

Consider:

```js
//console.log(aLet)  // would throw ReferenceError

let aLet;
console.log(aLet); // undefined
aLet = 10;
console.log(aLet); // 10
```

In this example the  **TDZ**  ends when  `aLet`  is declared, rather than assigned.

## What are the actual uses of ES6 WeakMap?
**WeakMaps**  provide a way to extend objects from the outside without interfering with garbage collection. Whenever you want to extend an object but can't because it is sealed - or from an external source - a WeakMap can be applied.

**WeakMap**  is only available for ES6 and above. A WeakMap is a collection of key and value pairs where the key must be an object.

```js
var map = new WeakMap();
var pavloHero = {
    first: "Pavlo",
    last: "Hero"
};
var gabrielFranco = {
    first: "Gabriel",
    last: "Franco"
};
map.set(pavloHero, "This is Hero");
map.set(gabrielFranco, "This is Franco");
console.log(map.get(pavloHero)); //This is Hero
```

The interesting aspect of the WeakMaps is the fact that it holds a weak reference to the key inside the map. A weak reference means that if the object is destroyed, the garbage collector will remove the entire entry from the WeakMap, thus freeing up memory.

## Explain why the following doesn't work as an IIFE. What needs to be changed to properly make it an IIFE?
```js
function foo(){ }();
```
IIFE stands for Immediately Invoked Function Expressions. The JavaScript parser reads  `function foo(){ }();`  as  `function foo(){ }`  and  `();`, where the former is a function declaration and the latter (a pair of brackets) is an attempt at calling a function but there is no name specified, hence it throws  `Uncaught SyntaxError: Unexpected token )`.

Here are two ways to fix it that involves adding more brackets:  `(function foo(){ })()`  and  `(function foo(){ }())`. These functions are not exposed in the global scope and you can even omit its name if you do not need to reference itself within the body.

You might also use  `void`  operator:  `void function foo(){ }();`. Unfortunately, there is one issue with such approach. The evaluation of given expression is always  `undefined`, so if your IIFE function returns anything, you can't use it. An example:

```js
// Don't add JS syntax to this code block to prevent Prettier from formatting it.
const foo = void
function bar() {
    return 'foo';
}();

console.log(foo); // undefined
```


## Explain about Webpack and the benefits of using Webpack?
Webpack is used to bundle javascript files that can be used in a browser. Webpack processes the application and builds a dependency graph to map each module of the project requirement and generated the bundles. It allows you to run that environment which has been hosted babel. The advantage of using a web pack is that it bundles multiple modules and packs into a single JavaScript file. It integrated the dev server which helps in updating code and asset management.

## What are template literals in Es6? 
Template literals are the string with embedded code and variables inside. Template literal allows concatenation and interpolation in much more comprehensive and clear in comparison with prior versions of ECMAScript. Let see an example of concatenating a string in JavaScript. 
```js
var a="Hello"; 
var b="John"; 
var c = a+ " " + b; 
Console.log(c); 
//outputs Hello John;
```
 In ES6 concatenation and interpolation is done by backtick “ in a single line. To interpolate a variable simply put in to {} braces forwarded by $ sign.>/p> // In ES6 
 ```js
let a="Hello"; 
let b="John"; 
let c=`${a} ${b}`; 
console.log(c); //outputs Hello John;
```

## Explain Destructuring Assignment in ES6?
Destructing assignment in another improvement in Es6. It allows us to extract data from array and objects into separate variables. Example 
```js
let full_name =['John','Deo']; 
let [first_name,last_name]=full_name;
console.log(first_name,last_name); 
// outputs John Deo 
```
Another example 
```js
let c=[100,200,330,400]; 
let [a,...b]=c; 
console.log(a,b); 
// outputs 100 [200, 330, 400]
```
## What is Set in ES6? 
Set is a collection of unique values. The values could be also primitives or object references. 
Creating a Set in Javascript 
```
let set = new Set(); 
set.add(1); 
set.add('1'); 
set.add({ key: 'value' }); 
console.log(set); 
// Set {1, '1', Object {key: 'value'}} 
```
## Explain Generator function in ES6? 
Generators are functions that can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances. A function keyword followed by an asterisk defines a generator function, which returns a Generator object. 
Generator Function Example. 
```
function* generator(i) { 
	yield i; 
	yield i + 10; 
} 
var gen = generator(10); 
console.log(gen.next().value); 
// expected output: 10 console.log(gen.next().value);
```
## Explain WeakMap in ES6? 
WeakMaps provide a way to extend objects from the outside without interfering with garbage collection. Whenever you want to extend an object but can't because it is sealed - or from an external source - a WeakMap can be applied. WeakMap was also introduced by ES6 in 2015

## What are Constants in ES6?
Constants are also referred to as Immutable variables. It means that the value of a constant variable cannot be changed. The value that has been assigned at the time of the declaration remains unchanged. For e.g. const X= 5.0, here the value of X remains 5 every time and it cannot be changed.

## What are Block Scoped variables and functions?
 The variables and functions are defined as indefinite blocks. It means these can be used where the variables and functions are defined or declared. If we have declared variable and function in any function block then their scope will be limit to that function only, they cannot be accessible outside the block/function. ‘Const’ keyword cannot change the value of a variable. ‘let’ keyword allows variable value to be re-assigned, it can be in for loop or arrays.

## Explain about Default parameter values, Rest parameter, Spread operator?
**Default parameter** values are used to initialize the functions with default values. The value of a parameter can be anything like a null value, number or function.  
The **rest parameter** is used to retrieve all the arguments to invoke the function. It means we can push the items of different categories separately. The rest parameter uses the rest parameter to combine parameters into a single array parameter.  
A **spread operator** is donated by … and then the variable name has been provided. E.g. ‘…X’ syntax of spread operator. It has been used to manipulate objects and array in ES6 and to copy the enumerable properties from one object to another.

## What are  `ES6 Modules`?
**Modules**  lets us split our code base to multiple files for more maintainability and this lets us avoid putting all of our code in one big file (yucksss). Before ES6 has supported Modules there were two popular module systems that were used for Code Maintainability in  **JavaScript**.

-   CommonJS -  **Nodejs**
-   AMD (Asynchronous Module Definition) -  **Browsers**

Basically, the sytanx for using modules are straightforward,  
`import`  is used for  _getting_  functionality from another file or several functionalities or values while  
`export`  is used for  _exposing_  functionality from a file or several functionalities or values.
## What are  **Promises**?
**Promises**  are one way in handling asynchronous operations in  **JavaScript**. It represents the value of an asynchronous operation.  **Promises**  was made to solve the problem of doing and dealing with async code before promises we're using callbacks.  

```
fs.readFile('somefile.txt', function (e, data) {
  if (e) {
    console.log(e);
  }
  console.log(data);
});

```

The problem with this approach if we have another async operation inside the callback and another. We will have a code that is messy and unreadable. This code is called  **Callback Hell**.  

```
//Callback Hell yucksss
fs.readFile('somefile.txt', function (e, data) {
  //your code here
  fs.readdir('directory', function (e, files) {
    //your code here
    fs.mkdir('directory', function (e) {
      //your code here
    })
  })
})

```

If we use promises in this code it will be more readable and easy to understand and easy to maintain.  

```
promReadFile('file/path')
  .then(data => {
    return promReaddir('directory');
  })
  .then(data => {
    return promMkdir('directory');
  })
  .catch(e => {
    console.log(e);
  })

```

Promises have 3 different states.

**Pending**  - The initial state of a promise. The promise's outcome has not yet been known because the operation has not been completed yet.

**Fulfilled**  - The async operation is completed and successful with the resulting value.

**Rejected**  - The async operation has failed and has a  _reason_  on why it failed.

**Settled**  - If the promise has been either  **Fulfilled**  or  **Rejected**.

The  **Promise**  constructor has two parameters which are functions  `resolve`  and  `reject`  respectively.  
If the async operation has been completed without errors call the  `resolve`  function to resolve the promise or if an error occurred  
call the  `reject`  function and pass the error or reason to it.  
We can access the result of the fulfilled promise using the  `.then`  
method and we catch errors in the  `.catch`  method. We chain multiple async promise operations in the  `.then`  method because the  `.then`  method returns a  **Promise**  just like the example in the imag e above.  

```
const myPromiseAsync = (...args) => {
  return new Promise((resolve, reject) => {
    doSomeAsync(...args, (error, data) => {
      if (error) {
        reject(error);
      } else {
        resolve(data);
      }
    })
  })
}

myPromiseAsync()
  .then(result => {
    console.log(result);
  })
  .catch(reason => {
    console.log(reason);
  })

```

We can make a helper func that converts an async operation with a callback to promise. It works like the  **promisify**  utility function from the node core module  `util`.  

```
const toPromise = (asyncFuncWithCallback) => {
  return (...args) => {
    return new Promise((res, rej) => {
      asyncFuncWithCallback(...args, (e, result) => {
        return e ? rej(e) : res(result);
      });
    });
  }
}

const promReadFile = toPromise(fs.readFile);

promReadFile('file/path')
  .then((data) => {
    console.log(data);
  })
  .catch(e => console.log(e));
```


## What is  _async/await_  and How does it work?
 _async/await_  is the new way of writing asynchronous or non-blocking code in  **JavaScript's**. It is built on top of  **Promises**. It makes writing asynchronous code more readable and cleaner than  
**Promise**s . But you must learn the basics of  **Promises**  before using this feature because as I said earlier it is built on top of  **Promises**  which means is still uses  **Promises**  under the hood.

Using Promises.  

```
function callApi() {
  return fetch("url/to/api/endpoint")
    .then(resp => resp.json())
    .then(data => {
      //do something with "data"
    }).catch(err => {
      //do something with "err"
    });
}


```

Using Async/Await.

**Note**: We're using the old  _try/catch_  statement to  **catch**  any errors that happened in any of those async operations inside the  _try_  statement.  

```
async function callApi() {
  try {
    const resp = await fetch("url/to/api/endpoint");
    const data = await resp.json();
    //do something with "data"
  } catch (e) {
    //do something with "err"
  }
}

```

**Note**: The  _async_  keyword before the function declaration makes the function return  _implicitly_  a  **Promise**.  

```
const giveMeOne = async () => 1;

giveMeOne()
  .then((num) => {
    console.log(num); // logs 1
  });

```

**Note**: The  _await_  keyword can  **only**  be used inside an  **async function**. Using  _await_  keyword in any other function which is not an  **async function**  will throw an error. The  _await_  keyword  **awaits**  the right-hand side expression (presumably a  **Promise**) to return before executing the next line of code.  

```
const giveMeOne = async () => 1;

function getOne() {
  try {
    const num = await giveMeOne();
    console.log(num);
  } catch (e) {
    console.log(e);
  }
}

//Throws a Compile-Time Error = Uncaught SyntaxError: await is only valid in an async function

async function getTwo() {
  try {
    const num1 = await giveMeOne(); //finishes this async operation first before going to
    const num2 = await giveMeOne(); //this line
    return num1 + num2;
  } catch (e) {
    console.log(e);
  }
}

await getTwo(); // returns 2
```

## What are  **Default Parameters**?
 **Default Parameters**  is a new way of defining default variables in  **JavaScript**  it is available in the  **ES6**  or  **ECMAScript 2015**  Version.  

```
//ES5 Version
function add(a,b){
  a = a || 0;
  b = b || 0;
  return a + b;
}

//ES6 Version
function add(a = 0, b = 0){
  return a + b;
}
//If we don't pass any argument for 'a' or 'b' then 
// it's gonna use the "default parameter" value which is 0
add(1); // returns 1 

```

We can also use Destructuring  in  **Default Paremeters**.  

```
function getFirst([first, ...rest] = [0, 1]) {
  return first;
}

getFirst();  // returns 0
getFirst([10,20,30]);  // returns 10

function getArr({ nums } = { nums: [1, 2, 3, 4] }){
    return nums;
}

getArr(); // returns [1, 2, 3, 4]
getArr({nums:[5,4,3,2,1]}); // returns [5,4,3,2,1]

```

We can also use the parameters defined first to the parameters defined after them.  

```
function doSomethingWithValue(value = "Hello World", callback = () => { console.log(value) }) {
  callback();
}
doSomethingWithValue(); //logs "Hello World"
```