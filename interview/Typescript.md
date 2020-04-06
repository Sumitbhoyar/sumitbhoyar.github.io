# Typescript

## What are different components of TypeScript?

There are mainly 3 components of TypeScript .

1.  **Language**  – The most important part for developers is the new language. The language consist of new syntax, keywords and allows you to write TypeScript.
2.  **Compiler**  – The TypeScript compiler is open source, cross-platform and open specification, and is written in TypeScript. Compiler will compile your TypeScript into JavaScript. And it will also emit error, if any. It can also help in concating different files to single output file and in generating source maps.
3.  **Language Service**  – TypeScript language service which powers the interactive TypeScript experience in Visual Studio,  VS Code, Sublime, the TypeScript playground and other editor.

## Which are the different data types supported by TypeScript?

TypeScript supports following data types.

-   Boolean  `var bValue: boolean = false;`
-   Number  `var age: number = 16;`
-   String  `var name: string = "jon";`
-   Array  `var list:number[] = [1, 2, 3];`
-   Enum
    
 `enum Color {Red, Green, Blue};`
 `var` `c: Color = Color.Green;`
    
-   Any  `var unknownType: any = 4;`
-   Void
    `function` `NoReturnType(): void {`
    
    `}`

## How TypeScript is optionally statically typed language?
TypeScript is referred as optionally statically typed, which means you can ask the compiler to ignore the type of a variable. Using  `any`  data type, we can assign any type of value to the variable. TypeScript will not give any error checking during compilation.
```
var unknownType: any = 4;
unknownType = "Okay, I am a string";
unknownType = false; // A boolean.
```

## Can an `interface` extends a `class` just like a `class` implements `interface`?

Yes, an  `interface`  extends a  `class`, when it does it inherits the members of the class but not their implementations. Interfaces inherit even the private and protected members of a base class. This means that when you create an interface that extends a class with private or protected members, that interface type can only be implemented by that class or a subclass of it.

## What are all the other access modifiers that TypeScript supports?

TypeScript supports access modifiers  `public`,  `private`  and  `protected`  which determine the accessibility of a  `class`  member as given below:

-   `public`  - All the members of the class, its child classes, and the instance of the class can access.
-   `protected`  - All the members of the class and its child classes can access them. But the instance of the class can not access.
-   `private`  - Only the members of the class can access them.

If an access modifier is not specified it is implicitly  `public`  as that matches the convenient nature of JavaScript.

Also note that at runtime (in the generated JS) these have no significance but will give you compile time errors if you use them incorrectly.

## What is Generic Class?
A generic class has a similar shape to a generic interface. Generic classes have a generic type parameter list in angle brackets (`<>`) following the name of the class.
```js
/** A class definition with a generic parameter */
class Queue<T> {
  private data = [];
  push = (item: T) => this.data.push(item);
  pop = (): T => this.data.shift();
}

const queue = new Queue<number>();
queue.push(0);
queue.push("1"); // ERROR : cannot push a string. Only numbers allowed
```

## What is getters/setters in TypeScript?
TypeScript supports  **getters/setters**  as a way of intercepting accesses to a member of an object. This gives you a way of having finer-grained control over how a member is accessed on each object.

```js
class foo {
  private _bar:boolean = false;

  get bar():boolean {
    return this._bar;
  }
  set bar(theBar:boolean) {
    this._bar = theBar;
  }
}

var myBar = myFoo.bar;  // correct (get)
myFoo.bar = true;  // correct (set)
```

## Explain how and why we could use property decorators in TS?
Decorators can be used to modify the behavior of a class or become even more powerful when integrated into a framework. For instance, if your framework has methods with restricted access requirements (just for admin), it would be easy to write an  `@admin`  method decorator to deny access to non-administrative users, or an  `@owner`  decorator to only allow the owner of an object the ability to modify it.

```ts
class CRUD {
    get() { }
    post() { }

    @admin
    delete() { }

    @owner
    put() { }
}
```
## How can you allow classes defined in a module to accessible outside of the module?
Classes define in a module are available within the module. Outside the module you can’t access them.
To make classes accessible outside module use `export` keyword for classes.

## Does TypeScript supports function overloading?
Yes, TypeScript does support function overloading but the implementation is a bit different if we compare it to OO languages. We are creating just one function and a number of declarations so that TypeScript doesn't give compile errors. When this code is compiled to JavaScript, the concrete function alone will be visible. As a JavaScript function can be called by passing multiple arguments, it just works.

```js
class Foo {
    myMethod(a: string);
    myMethod(a: number);
    myMethod(a: number, b: string);
    myMethod(a: any, b?: string) {
        alert(a.toString());
    }
}
```

## How does TypeScript support optional parameters in function as in JavaScript every parameter is optional for a function?
In JavaScript, every parameter is considered optional. If no value is supplied, then it is treated as `undefined`. So while writing functions in TypeScript, we can make a parameter optional using the **“?”** after the parameter name.
```
function Demo(arg1: number, arg2? :number) {
}
```
So, arg1 is always required and arg2 is optional parameter. Remember, **Optional parameters must follow required parameters.** If we want to make arg1 optional, instead of arg2 then we need to change the order and arg1 must be put after arg2.
```
function Demo(arg2: number, arg1? :number) {
}
```
Similar to optional parameters, default parameters are also supported.
```
function Demo(arg1: number, arg2 = 4) {
}
```

## What is TypeScript Declare Keyword?
It’s quite possible that JavaScript libraries/frameworks don’t have TypeScript definition files and yet you want to use them without any errors. Te solution is to use the `declare` keyword. The `declare` keyword is used for **ambient declarations** where you want to define a variable that may not have originated from a TypeScript file.
`declare var unKnownLibrary;`
TypeScript runtime will assign unKnownLibrary variable `any` type. You won’t get Intellisense in design time but you will be able to use the library in your code.

### What is tsconfig.json file?
The presence of a tsconfig.json file in a directory indicates that the directory is the root of a TypeScript project. The tsconfig.json file specifies the root files and the compiler options required to compile the project. And using this file we can streamline building TypeScript project. Below is a sample tsconfig.json file.
```
{
   "compilerOptions": {
      "removeComments": true,
      "sourceMap": true
   },
   "files": [
      "main.ts",
      "othermodule.ts"
    ]
}
```
Within files section, define all the .ts files in the project. And When invoke tsc without any other arguments with the above file in the current directory, it will compile all the files with the given compiler option settings.

## How do you implement inheritance in TypeScript?
```
class Shape {
	  Area:number
	  constructor(area:number) {
		  this.Area = area
	  }
}
class Circle extends Shape {
  display():void {
	  console.log("Area of the circle: "+this.Area)
  }
}
var obj = new Circle(320);
obj.display() //Output: Area of the circle: 320
```

## Internal Module vs  External Module 

| Internal Module | External Module |
|--|--|
| Internal modules were used to logically group the classes, interfaces, functions, variables into a single unit and can be exported in another module. | External modules are useful in hiding the internal statements of the module definitions and show only the methods and parameters associated with the declared variable. |
| Internal modules were in the earlier version of Typescript. But they are still supported by using namespace in the latest version of TypeScript. | External modules are simply known as a module in the latest version of TypeScript. |
| Internal modules are local or exported members of other modules (including the global module and external modules). | External modules are separately loaded bodies of code referenced using external module names. |
| Internal modules are declared using ModuleDeclarations that specify their name and body. | An external module is written as a separate source file that contains at least one import or export declaration. |

Internal Module - Example
```
module Sum {   
   export function add(a, b) {    
      console.log("Sum: " +(a+b));   
   }   
}
```
External Module - Example
```
export class Addition{  
    constructor(private x?: number, private y?: number){  
    }  
    Sum(){  
        console.log("SUM: " +(this.x + this.y));  
    }  
}
```
## Explain generics in TypeScript?

TypeScript Generics is a tool which provides a way to create reusable components. It is able to create components that can work with a variety of data types rather than a single data type. Generics provides type safety without compromising the performance, or productivity. Generics allow us to create generic classes, generic functions, generic methods, and generic interfaces.

In generics, a type parameter is written between the open (<) and close (>) brackets which makes it strongly typed collections. Generics use a special kind of type variable <T> that denotes types. The generics collections contain only similar types of objects.
```
function identity<T>(arg: T): T {
	return arg;
}
let output1 = identity<string>("myString");
let output2 = identity<number>( 100 );
console.log(output1);
console.log(output2);
```

## Explain Relative vs. Non-relative module imports.
| Non-Relative | Relative |
|--|--|
| A non-relative import can be resolved relative to baseUrl, or through path mapping. In other words, we use non-relative paths when importing any of our external dependencies. | Relative imports can be used for our own modules that are guaranteed to maintain their relative location at runtime. A relative import is starts with /, ./ or ../. |
| import * as $ from "jquery"; | import Entry from "./components/Entry"; |
| import { Component } from "@angular/core"; | import {DefaultHeaders} from "../constants/http"; |