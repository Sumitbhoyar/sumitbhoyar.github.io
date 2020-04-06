# JavaScript

## What's the difference between  `undefined`  and  `null`?.

Before understanding the differences between  `undefined`  and  `null`  we must understand the similarities between them.

-   They belong to  **JavaScript's**  7 primitive types.

```
 let primitiveTypes = ['string','number','null','undefined','boolean','symbol', 'bigint'];

```

-   They are  **falsy**  values. Values that evaluated to false when converting it to boolean using  `Boolean(value)`  or  `!!value`.

```
   console.log(!!null); //logs false
   console.log(!!undefined); //logs false

   console.log(Boolean(null)); //logs false
   console.log(Boolean(undefined)); //logs false

```

Ok, let's talk about the differences.

-   `undefined`  is the default value of a variable that has not been assigned a specific value. Or a function that has no  **explicit**  return value ex.  `console.log(1)`. Or a property that does not exist in an object. The JavaScript engine does this for us the  **assigning**  of  `undefined`  value.

```
  let _thisIsUndefined;
  const doNothing = () => {};
  const someObj = {
    a : "ay",
    b : "bee",
    c : "si"
  };

  console.log(_thisIsUndefined); //logs undefined
  console.log(doNothing()); //logs undefined
  console.log(someObj["d"]); //logs undefined

```

-   `null`  is  **"a value that represents no value"**.  `null`  is value that has been  **explicitly**  defined to a variable. In this example we get a value of  `null`  when the  `fs.readFile`  method does not throw an error.

```
  fs.readFile('path/to/file', (e,data) => {
     console.log(e); //it logs null when no error occurred
     if(e){
       console.log(e);
     }
     console.log(data);
   });

```

When comparing  `null`  and  `undefined`  we get  `true`  when using  `==`  and  `false`  when using  `===`. You can read the reason  [here](https://dev.to/macmacky/70-javascript-interview-questions-5gfi#14-whats-the-difference-between-and-).  

```
   console.log(null == undefined); // logs true
   console.log(null === undefined); // logs false
```

## What is  **Event Propagation**?
When an  **event**  occurs on a  **DOM**  element, that  **event**  does not entirely occur on that just one element. In the  **Bubbling Phase**, the  **event**  bubbles up or it goes to its parent, to its grandparents, to its grandparent's parent until it reaches all the way to the  `window`  while in the  **Capturing Phase**  the event starts from the  `window`  down to the element that triggered the event or the  `event.target`.

**Event Propagation**  has  **three**  phases.

1.  Capturing Phase  – the event starts from  `window`  then goes down to every element until it reaches the target element.
2.  Target Phase  – the event has reached the target element.
3.  Bubbling Phase  – the event bubbles up from the target element then goes up every element until it reaches the  `window`.

## What's  **Event Bubbling**?
When an  **event**  occurs on a  **DOM**  element, that  **event**  does not entirely occur on that just one element. In the  **Bubbling Phase**, the  **event**  bubbles up or it goes to its parent, to its grandparents, to its grandparent's parent until it reaches all the way to the  `window`.
If we click on the `child` element it logs `child`,`parent`,`grandparent`, `html`, `document` and `window` respectively on the **console**. This is **Event Bubbling**.

## What's the difference between  `==`  and  `===`  ?

The difference between  `==`**(abstract equality)**  and  `===`**(strict equality)**  is that the  `==`  compares by  **value**  after  _coercion_  and  `===`  compares by  **value**  and  **type**  without  _coercion_.

Let's dig deeper on the  `==`. So first let's talk about  _coercion_.

_coercion_  is the process of converting a value to another type. As in this case, the  `==`  does  _implicit coercion_. The  `==`  has some conditions to perform before comparing the two values.

Suppose we have to compare  `x == y`  values.

1.  If  `x`  and  `y`  have same type. Then compare them with the  `===`  operator.
2.  If  `x`  is  `null`  and  `y`  is  `undefined`  then return  `true`.
3.  If  `x`  is  `undefined`  and  `y`  is  `null`  then return  `true`.
4.  If  `x`  is type  `number`  and  `y`  is type  `string`  Then return  `x == toNumber(y)`.
5.  If  `x`  is type  `string`  and  `y`  is type  `number`  Then return  `toNumber(x) == y`.
6.  If  `x`  is type  `boolean`  Then return  `toNumber(x) == y`.
7.  If  `y`  is type  `boolean`  Then return  `x == toNumber(y)`.
8.  If  `x`  is either  `string`,`symbol`  or  `number`  and  `y`  is type  `object`  Then return  `x == toPrimitive(y)`.
9.  If  `x`  is either  `object`  and  `x`  is either  `string`,`symbol`  Then return  `toPrimitive(x) == y`.
10.  Return  `false`.

**Note:**  `toPrimitive`  uses first the  `valueOf`  method then the  `toString`  method in objects to get the primitive value of that object.

Let's have examples.
| `x` | `y` | `x == y` |
|--|--|--|
| `5` | `5` | `true` |
| `1` | `'1'` | `true` |
| `null` | `undefined` | `true` |
| `0` | `false` | `true` |
| `'1,2'` | `[1,2]` | `true` |
| `'[object Object]'` | `{}` | `true` |

These examples all return  `true`.

The  **first example**  goes to  **condition one**  because  `x`  and  `y`  have the same type and value.

The  **second example**  goes to  **condition four**  `y`  is converted to a  `number`  before comparing.

The  **third example**  goes to  **condition two**.

The  **fourth example**  goes to  **condition seven**  because  `y`  is  `boolean`.

The  **fifth example**  goes to  **condition eight**. The array is converted to a  `string`  using the  `toString()`  method which returns  `1,2`.

The  **last example**  goes to  **condition ten**. The object is converted to a  `string`  using the  `toString()`  method which returns  `[object Object]`.

Let's have examples.
| `x` | `y` | `x == y` |
|--|--|--|
| `5` | `5` | `true` |
| `1` | `'1'` | `false`|
| `null` | `undefined` | `false` |
| `0` | `false` | `false` |
| `'1,2'` | `[1,2]` | `false` |
| `'[object Object]'` | `{}` | `false` |

If we use the  `===`  operator all the comparisons except for the first example will return  `false`  because they don't have the same type while the first example will return  `true`  because the two have the same type and value.


## Why does it return  **false**  when comparing two similar objects in JavaScript?
Suppose we have an example below.  
```
let a = { a: 1 };
let b = { a: 1 };
let c = a;

console.log(a === b); // logs false even though they have the same property
console.log(a === c); // logs true hmm
```
**JavaScript**  compares  _objects_  and  _primitives_  differently. In  _primitives_  it compares them by  **value**  while in  _objects_  it compares them by  **reference**  or the  **address in memory where the variable is stored**. That's why the first  `console.log`  statement returns  `false`  and the second  `console.log`  statement returns  `true`.  `a`  and  `c`  have the same reference and  `a`  and  `b`  are not.

## What does the  **!!**  operator do?

The  **Double NOT**  operator or  **!!**  coerces the value on the right side into a boolean. basically it's a fancy way of converting a value into a boolean.  
```
console.log(!!null); //logs false
console.log(!!undefined); //logs false
console.log(!!''); //logs false
console.log(!!0); //logs false
console.log(!!NaN); //logs false
console.log(!!' '); //logs true
console.log(!!{}); //logs true
console.log(!![]); //logs true
console.log(!!1); //logs true
console.log(!![].length); //logs false
```
## How to evaluate multiple expressions in one line?
We can use the  `,`  or comma operator to evaluate multiple expressions in one line. It evaluates from left-to-right and returns the value of the last item on the right or the last operand.  
```
let x = 5;

x = (x++ , x = addFive(x), x *= 2, x -= 5, x += 10);

function addFive(num) {
  return num + 5;
}
```
If you log the value of  `x`  it would be  **27**. First, we  **increment**  the value of x it would be  **6**, then we invoke the function  `addFive(6)`  and pass the 6 as a parameter and assign the result to  `x`  the new value of  `x`  would be  **11**. After that, we multiply the current value of  `x`  to  **2**  and assign it to  `x`  the updated value of  `x`  would be  **22**. Then, we subtract the current value of  `x`  to 5 and assign the result to  `x`  the updated value would be  **17**. And lastly, we increment the value of  `x`  by 10 and assign the updated value to  `x`  now the value of  `x`  would be  **27**.

## What is  **Scope**?
**Scope**  in JavaScript is the  **area**  where we have valid access to variables or functions. JavaScript has three types of Scopes.  **Global Scope**,  **Function Scope**, and  **Block Scope(ES6)**.

-   **Global Scope**  - variables or functions declared in the global namespace are in the global scope and therefore is accessible everywhere in our code.

```
   //global namespace
   var g = "global";

   function globalFunc(){
     function innerFunc(){
          console.log(g); // can access "g" because "g" is a global variable
     }
     innerFunc();
   }  

```

-   **Function Scope**  - variables,functions and parameters declared within a function are accessible inside that function but not outside of it.

```
    function myFavoriteFunc(a) {
       if (true) {
          var b = "Hello " + a;
       }
       return b;
   }
   myFavoriteFunc("World");

   console.log(a); // Throws a ReferenceError "a" is not defined
   console.log(b); // does not continue here 

```

-   **Block Scope**  - variables  **(`let`,`const`)**  declared within a block  `{}`  can only be access within it.

```
 function testBlock(){
   if(true){
     let z = 5;
   }
   return z; 
 }

 testBlock(); // Throws a ReferenceError "z" is not defined

```

**Scope**  is also a set of rules for finding variables. If a variable does not exist in the  **current scope**  it  **look ups**  and searches for a variable in the  **outer scope**  and if does not exist again it  **looks up**  again until it reaches the  **global scope**  if the variable exists then we can use it if not it throws an error. It searches for the  **nearest**  variable and it stops  **searching**  or  **looking up**  once it finds it. This is called  **Scope Chain**.  

```
   /* Scope Chain
   Inside inner function perspective

   inner's scope -> outer's scope -> global's scope
  */


  //Global Scope
  var variable1 = "Comrades";   
  var variable2 = "Sayonara";

  function outer(){
  //outer's scope
    var variable1 = "World";
    function inner(){
    //inner's scope
      var variable2 = "Hello";
      console.log(variable2 + " " + variable1);
    }
    inner();
  }  
  outer(); 
// logs Hello World 
// because (variable2 = "Hello") and (variable1 = "World") are the nearest 
// variables inside inner's scope.
```

## What are the  **falsy**  values in  **JavaScript**?
```
 const falsyValues = ['', 0, null, undefined, NaN, false];

```

**falsy**  values are values that when converted to boolean becomes  **false**.

## How to check if a value is  **falsy**?
Use the  **Boolean**  function or the Double NOT operator  **[!!]**

## What does  `"use strict"`  do?
`"use strict"`  is a ES5 feature in  **JavaScript**  that makes our code in  **Strict Mode**  in  _functions_  or  _entire scripts_.  **Strict Mode**  helps us avoid  **bugs**  early on in our code and adds restrictions to it.

Restrictions that  **Strict Mode**  gives us.

-   Assigning or Accessing a variable that is not declared.

```
 function returnY(){
    "use strict";
    y = 123;
    return y;
 }

```

-   Assigning a value to a read-only or non-writable global variable;

```
   "use strict";
   var NaN = NaN;
   var undefined = undefined;
   var Infinity = "and beyond";

```

-   Deleting an undeletable property.

```
   "use strict";
   const obj = {};

   Object.defineProperty(obj, 'x', {
      value : '1'
   });  

   delete obj.x;

```

-   Duplicate parameter names.

```
   "use strict";

   function someFunc(a, b, b, c){

   }

```

-   Creating variables with the use of the  **eval**  function.

```
 "use strict";

 eval("var x = 1;");

 console.log(x); //Throws a Reference Error x is not defined


```

-   The default value of  **this**  will be  `undefined`.

```
  "use strict";

  function showMeThis(){
    return this;
  }

  showMeThis(); //returns undefined

```

There are many more restrictions in  **Strict Mode**  than these.


## What's the value of  `this`  in JavaScript?
Basically,  `this`  refers to the value of the object that is currently executing or invoking the function. I say  **currently**  due to the reason that the value of  **this**  changes depending on the context on which we use it and where we use it.  

```
   const carDetails = {
     name: "Ford Mustang",
     yearBought: 2005,
     getName(){
        return this.name;
     },
     isRegistered: true
   };

   console.log(carDetails.getName()); // logs Ford Mustang

```

This is what we would normally expect because in the  **getName**  method we return  `this.name`,  `this`  in this context refers to the object which is the  `carDetails`  object that is currently the "owner" object of the function executing.

Ok, Let's some add some code to make it weird. Below the  `console.log`  statement add this three lines of code  

```
   var name = "Ford Ranger";
   var getCarName = carDetails.getName;

   console.log(getCarName()); // logs Ford Ranger

```

The second  `console.log`  statement prints the word  **Ford Ranger**  which is weird because in our first  `console.log`  statement it printed  **Ford Mustang**. The reason to this is that the  `getCarName`  method has a different "owner" object that is the  `window`  object. Declaring variables with the  `var`  keyword in the global scope attaches properties in the  `window`  object with the same name as the variables. Remember  `this`  in the global scope refers to the  `window`  object when  `"use strict"`  is not used.  

```
  console.log(getCarName === window.getCarName); //logs true
  console.log(getCarName === this.getCarName); // logs true

```

`this`  and  `window`  in this example refer to the same object.

One way of solving this problem is by using the  `apply`  methods in functions.  

```
   console.log(getCarName.apply(carDetails)); //logs Ford Mustang
   console.log(getCarName.call(carDetails));  //logs Ford Mustang

```

The  `apply`  and  `call`  methods expects the first parameter to be an object which would be value of  `this`  inside that function.

**IIFE**  or  **Immediately Invoked Function Expression**, Functions that are declared in the global scope,  **Anonymous Functions**  and Inner functions in methods inside an object has a default of  **this**  which points to the  **window**  object.  

```
   (function (){
     console.log(this);
   })(); //logs the "window" object

   function iHateThis(){
      console.log(this);
   }

   iHateThis(); //logs the "window" object  

   const myFavoriteObj = {
     guessThis(){
        function getName(){
          console.log(this.name);
        }
        getName();
     },
     name: 'Marko Polo',
     thisIsAnnoying(callback){
       callback();
     }
   };


   myFavoriteObj.guessThis(); //logs the "window" object
   myFavoriteObj.thisIsAnnoying(function (){
     console.log(this); //logs the "window" object
   });

```

If we want to get the value of the  `name`  property which is  **Marko Polo**  in the  `myFavoriteObj`  object there are two ways to solve this.

First, we save the value of  `this`  in a variable.  

```
   const myFavoriteObj = {
     guessThis(){
         const self = this; //saves the this value to the "self" variable
         function getName(){
           console.log(self.name);
         }
         getName();
     },
     name: 'Marko Polo',
     thisIsAnnoying(callback){
       callback();
     }
   };

```

In this image we save the value of  `this`  which would be the  `myFavoriteObj`  object. So we can access it inside the  `getName`  inner function.

Second, we use  **ES6  Arrow Functions**.  

```
   const myFavoriteObj = {
     guessThis(){
         const getName = () => { 
           //copies the value of "this" outside of this arrow function
           console.log(this.name);
         }
         getName();
     },
     name: 'Marko Polo',
     thisIsAnnoying(callback){
       callback();
     }
   };

```

Arrow Functions  does not have its own  `this`. It copies the value of  `this`  of the enclosing lexical scope or in this example the value of  `this`  outside the  `getName`  inner function which would be the  `myFavoriteObj`  object.

## What is the use  `Function.prototype.apply`  method?
The  `apply`  invokes a function specifying the  `this`  or the "owner" object of that function on that time of invocation.  

```
const details = {
  message: 'Hello World!'
};

function getMessage(){
  return this.message;
}

getMessage.apply(details); // returns 'Hello World!'

```

This method works like  `Function.prototype.call`  the only difference is how we pass arguments. In  `apply`  we pass arguments as an array.  

```
const person = {
  name: "Marko Polo"
};

function greeting(greetingMessage) {
  return `${greetingMessage} ${this.name}`;
}

greeting.apply(person, ['Hello']); // returns "Hello Marko Polo!"

```

## What is the use  `Function.prototype.call`  method?
The  `call`  invokes a function specifying the  `this`  or the "owner" object of that function on that time of invocation.  

```
const details = {
  message: 'Hello World!'
};

function getMessage(){
  return this.message;
}

getMessage.call(details); // returns 'Hello World!'

```

This method works like  `Function.prototype.apply`  the only difference is how we pass arguments. In  `call`  we pass directly the arguments separating them with a comma  `,`  for every argument.  

```
const person = {
  name: "Marko Polo"
};

function greeting(greetingMessage) {
  return `${greetingMessage} ${this.name}`;
}

greeting.call(person, 'Hello'); // returns "Hello Marko Polo!"

```

## What's the difference between  `Function.prototype.apply`  and  `Function.prototype.call`?
The only difference between  `apply`  and  `call`  is how we pass the  **arguments**  in the function being called. In  `apply`  we pass the arguments as an  **array**  and in  `call`  we pass the arguments directly in the argument list.  

```
const obj1 = {
 result:0
};

const obj2 = {
 result:0
};

function reduceAdd(){
   let result = 0;
   for(let i = 0, len = arguments.length; i < len; i++){
     result += arguments[i];
   }
   this.result = result;
}

reduceAdd.apply(obj1, [1, 2, 3, 4, 5]); // returns 15
reduceAdd.call(obj2, 1, 2, 3, 4, 5); // returns 15
```

## What are  **Higher Order Functions**?
**Higher-Order Function**  are functions that can return a function or receive argument or arguments which has a value of a function.  

```
function higherOrderFunction(param,callback){
    return callback(param);
}
```

## What are  **Arrow functions**?
**Arrow Functions**  are a new way of making functions in JavaScript.  **Arrow Functions**  takes a little time in making functions and has a cleaner syntax than a  **function expression**  because we omit the  `function`  keyword in making them.  

```
//ES5 Version
var getCurrentDate = function (){
  return new Date();
}

//ES6 Version
const getCurrentDate = () => new Date();

```

In this example, in the ES5 Version have  `function(){}`  declaration and  `return`  keyword needed to make a function and return a value respectively. In the  **Arrow Function**  version we only need the  `()`  parentheses and we don't need a  `return`  statement because  **Arrow Functions**  have a implicit return if we have only one expression or value to return.  

```
//ES5 Version
function greet(name) {
  return 'Hello ' + name + '!';
}

//ES6 Version
const greet = (name) => `Hello ${name}`;
const greet2 = name => `Hello ${name}`;


```

We can also parameters in  **Arrow functions**  the same as the  **function expressions**  and  **function declarations**. If we have one parameter in an  **Arrow Function**  we can omit the parentheses it is also valid.  

```
const getArgs = () => arguments

const getArgs2 = (...rest) => rest

```

**Arrow functions**  don't have access to the  `arguments`  object. So calling the first  `getArgs`  func will throw an Error. Instead we can use the  **rest parameters**  to get all the arguments passed in an arrow function.  

```
const data = {
  result: 0,
  nums: [1, 2, 3, 4, 5],
  computeResult() {
    // "this" here refers to the "data" object
    const addAll = () => {
      // arrow functions "copies" the "this" value of 
      // the lexical enclosing function
      return this.nums.reduce((total, cur) => total + cur, 0)
    };
    this.result = addAll();
  }
};

```

**Arrow functions**  don't have their own  `this`  value. It captures or gets the  `this`  value of lexically enclosing function or in this example, the  `addAll`  function copies the  `this`  value of the  `computeResult`  method and if we declare an arrow function in the global scope the value of  `this`  would be the  `window`  object.




### What are  **Closures**?
**Closures**  is simply the ability of a function at the time of declaration to remember the references of variables and parameters on its current scope, on its parent function scope, on its parent's parent function scope until it reaches the global scope with the help of  **Scope Chain**. Basically it is the  **Scope**  created when the function was declared.

Examples are a great way to explain closures.  

```
   //Global's Scope
   var globalVar = "abc";

   function a(){
   //testClosures's Scope
     console.log(globalVar);
   }

   a(); //logs "abc" 
   /* Scope Chain
      Inside a function perspective

      a's scope -> global's scope  
   */ 

```

In this example, when we declare the  `a`  function the  **Global Scope**  is part of  `a's`  _closure_.

[![a's closure](https://res.cloudinary.com/practicaldev/image/fetch/s--gbH9Uqec--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/teatokuw4xvgtlzbzhn8.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--gbH9Uqec--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/teatokuw4xvgtlzbzhn8.png)

The reason for the variable  `globalVar`  which does not have a value in the image because of the reason that the value of that variable can change based on  **where**  and  **when**  we invoke the  `a`  function.  
But in our example above the  `globalVar`  variable will have the value of  **abc**.

Ok, let's have a complex example.  

```
var globalVar = "global";
var outerVar = "outer"

function outerFunc(outerParam) {
  function innerFunc(innerParam) {
    console.log(globalVar, outerParam, innerParam);
  }
  return innerFunc;
}

const x = outerFunc(outerVar);
outerVar = "outer-2";
globalVar = "guess"
x("inner");

```

[![Complex](https://res.cloudinary.com/practicaldev/image/fetch/s--inSFoNQU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/e4hxm7zvz8eun2ppenwp.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--inSFoNQU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/e4hxm7zvz8eun2ppenwp.png)  
This will print "guess outer inner". The explanation for this is that when we invoke the  `outerFunc`  function and assigned the returned value the  `innerFunc`  function to the variable  `x`, the  `outerParam`  will have a value of  **outer**  even though we assign a new value  **outer-2**  to the  `outerVar`  variable because  
the reassignment happened after the invocation of the  `outer`  function and in that time when we invoke the  `outerFunc`  function it's look up the value of  `outerVar`  in the  **Scope Chain**, the  `outerVar`  will have a value of  **"outer"**. Now, when we invoke the  `x`  variable which have a reference to the  `innerFunc`, the  
`innerParam`  will have a value of  **inner**  because thats the value we pass in the invocation and the  `globalVar`  variable will have a value of  **guess**  because before the invocation of the  `x`  variable we assign a new value to the  `globalVar`  and at the time of invocation  `x`  the value of  `globalVar`  in the__Scope Chain__ is  
**guess**.

We have an example that demonstrates a problem of not understanding closure correctly.  

```
const arrFuncs = [];
for(var i = 0; i < 5; i++){
  arrFuncs.push(function (){
    return i;
  });
}
console.log(i); // i is 5

for (let i = 0; i < arrFuncs.length; i++) {
  console.log(arrFuncs[i]()); // all logs "5"
}

```

This code is not working as we expected because of  **Closures**.  
The  `var`  keyword makes a global variable and when we push a function  
we return the global variable  `i`. So when we call one of those functions in that array after the loop it logs  `5`  because we get  
the current value of  `i`  which is  `5`  and we can access it because it's a global variable. Because  **Closures**  keeps the  **references**  of that variable not its  **values**  at the time of it's creation. We can solve this using  **IIFES**  or changing the  `var`  keyword to  `let`  for block-scoping.