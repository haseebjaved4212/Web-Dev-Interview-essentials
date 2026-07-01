# ⚡ JavaScript Interview Essentials

> A comprehensive, in-depth reference guide covering every JavaScript concept you need to ace frontend, backend, and full-stack developer interviews. From data types and closures to async/await, prototypes, design patterns, and performance — everything in one place.

---

## 📌 Table of Contents

- [What is JavaScript?](#what-is-javascript)
- [Data Types](#data-types)
- [Variables: var, let, const](#variables-var-let-const)
- [Type Coercion and Equality](#type-coercion-and-equality)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Scope and Closures](#scope-and-closures)
- [Hoisting](#hoisting)
- [The this Keyword](#the-this-keyword)
- [Prototypes and Inheritance](#prototypes-and-inheritance)
- [Classes](#classes)
- [Arrays and Array Methods](#arrays-and-array-methods)
- [Objects](#objects)
- [Destructuring](#destructuring)
- [Spread and Rest](#spread-and-rest)
- [Iterables and Iterators](#iterables-and-iterators)
- [Generators](#generators)
- [Symbols](#symbols)
- [Map, Set, WeakMap, WeakSet](#map-set-weakmap-weakset)
- [Error Handling](#error-handling)
- [Asynchronous JavaScript](#asynchronous-javascript)
- [Promises](#promises)
- [Async and Await](#async-and-await)
- [Event Loop](#event-loop)
- [DOM Manipulation](#dom-manipulation)
- [Events and Event Delegation](#events-and-event-delegation)
- [Fetch API and HTTP](#fetch-api-and-http)
- [Modules](#modules)
- [Design Patterns](#design-patterns)
- [Functional Programming Concepts](#functional-programming-concepts)
- [Memory Management and Garbage Collection](#memory-management-and-garbage-collection)
- [Performance Best Practices](#performance-best-practices)
- [Common Interview Questions](#common-interview-questions)

---

## What is JavaScript?

JavaScript is a **high-level, interpreted, dynamically-typed, single-threaded** programming language with a **non-blocking event loop** concurrency model. It is the only language that runs natively in the browser, and with Node.js it also runs on the server.

Key characteristics:
- **Dynamically typed** — types are determined at runtime, not compile time
- **Weakly typed** — implicit type coercion happens automatically
- **Prototype-based** — inheritance works through prototype chains
- **First-class functions** — functions are values, can be passed around like any other variable
- **Single-threaded** — one call stack, one thing at a time, but async via the event loop
- **Multi-paradigm** — supports procedural, object-oriented, and functional programming styles

---

## Data Types

JavaScript has **8 data types**: 7 primitives and 1 object type.

### Primitive Types

```javascript
// 1. Number (64-bit floating point, IEEE 754)
let age = 25;
let price = 9.99;
let negative = -42;
let scientific = 1.5e6;      // 1,500,000
let hex = 0xFF;              // 255
let binary = 0b1010;         // 10
let octal = 0o17;            // 15
let infinity = Infinity;
let nan = NaN;               // Not a Number (still typeof "number")

// 2. BigInt (integers beyond Number.MAX_SAFE_INTEGER)
let big = 9007199254740993n;
let bigCalc = 100n * 200n;   // Must combine BigInt with BigInt

// 3. String
let name = "Haseeb";
let template = `Hello, ${name}!`;
let multiline = `Line 1
Line 2`;

// 4. Boolean
let isActive = true;
let isLoggedIn = false;

// 5. undefined (variable declared but not assigned)
let x;
console.log(x); // undefined

// 6. null (intentional absence of value)
let user = null;

// 7. Symbol (unique, immutable identifier)
let id = Symbol("id");
let id2 = Symbol("id");
console.log(id === id2); // false (always unique)
```

### Object Type

```javascript
// Everything that is not a primitive is an object
let obj    = {};
let arr    = [];
let fn     = function() {};
let date   = new Date();
let regex  = /pattern/;
let map    = new Map();
```

### typeof Operator

```javascript
typeof 42           // "number"
typeof "hello"      // "string"
typeof true         // "boolean"
typeof undefined    // "undefined"
typeof null         // "object"  <-- famous bug, null is NOT an object
typeof Symbol()     // "symbol"
typeof 42n          // "bigint"
typeof {}           // "object"
typeof []           // "object"  <-- arrays are objects
typeof function(){} // "function"

// Better null check
value === null

// Better array check
Array.isArray([])   // true
```

> **Interview Tip:** `typeof null === "object"` is a historical bug from JavaScript's early days and has never been fixed for backward compatibility. Always use `=== null` to check for null.

---

## Variables: var, let, const

```javascript
// var: function-scoped, hoisted (with undefined), re-declarable
var x = 1;
var x = 2;   // no error
if (true) {
  var y = 10;
}
console.log(y); // 10 (leaks out of block)

// let: block-scoped, hoisted but NOT initialized (TDZ), not re-declarable
let a = 1;
// let a = 2; // SyntaxError: already declared
if (true) {
  let b = 10;
}
// console.log(b); // ReferenceError: b is not defined

// const: block-scoped, must be initialized, cannot be reassigned
const PI = 3.14159;
// PI = 3; // TypeError: Assignment to constant variable

// const with objects (the reference is constant, not the value)
const user = { name: "Haseeb" };
user.name = "Ahmed";    // allowed
user.age = 25;          // allowed
// user = {};           // TypeError: cannot reassign
```

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function | Block | Block |
| Hoisting | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Re-declarable | Yes | No | No |
| Re-assignable | Yes | Yes | No |
| Global property | Yes | No | No |

> **Interview Tip:** Always prefer `const` by default. Use `let` only when you know the variable will be reassigned. Never use `var` in modern code.

---

## Type Coercion and Equality

### Implicit Coercion

```javascript
// Number + String = String (concatenation)
1 + "2"        // "12"
"3" - 1        // 2 (subtraction converts to number)
"6" / "2"      // 3
"5" * "3"      // 15
true + 1       // 2
false + 1      // 1
null + 1       // 1
undefined + 1  // NaN

// Comparison coercion
"5" > 3        // true (string converted to number)
null == undefined  // true (special case)
null === undefined // false
NaN == NaN         // false (NaN is never equal to anything)
```

### == vs ===

```javascript
// == (loose equality): performs type coercion
0 == ""        // true
0 == false     // true
"" == false    // true
null == undefined // true
1 == "1"       // true

// === (strict equality): no coercion, checks type AND value
0 === ""       // false
0 === false    // false
1 === "1"      // false
null === undefined // false
```

### Falsy and Truthy Values

```javascript
// Falsy values (evaluate to false in boolean context)
false, 0, -0, 0n, "", '', ``, null, undefined, NaN

// Everything else is truthy
"0"        // truthy (non-empty string)
[]         // truthy (empty array)
{}         // truthy (empty object)
-1         // truthy
"false"    // truthy
```

```javascript
// Practical examples
if ("") { }          // does not run
if ([]) { }          // runs (gotcha!)
if (0) { }           // does not run
if ("0") { }         // runs

// Explicit conversion
Boolean("")          // false
Boolean([])          // true
Number(true)         // 1
Number(false)        // 0
Number(null)         // 0
Number(undefined)    // NaN
Number("")           // 0
Number("42px")       // NaN
String(42)           // "42"
String(null)         // "null"
```

---

## Operators

```javascript
// Arithmetic
+, -, *, /, %, **   // addition, subtraction, multiply, divide, modulo, exponent
2 ** 10              // 1024

// Assignment
=, +=, -=, *=, /=, %=, **=, &&=, ||=, ??=

// Logical
&&   // AND (returns first falsy or last value)
||   // OR  (returns first truthy or last value)
!    // NOT
??   // Nullish coalescing (returns right side only if left is null/undefined)

// Short circuit evaluation
false && doSomething()    // doSomething never called
true  || doSomething()    // doSomething never called

// Nullish coalescing vs OR
let count = 0;
let a = count || 10;   // 10 (because 0 is falsy)
let b = count ?? 10;   // 0  (because 0 is NOT null or undefined)

// Optional chaining
user?.profile?.avatar?.url   // undefined instead of TypeError
arr?.[0]                     // undefined if arr is null/undefined
fn?.()                       // only calls if fn is a function

// Ternary
let label = age >= 18 ? "Adult" : "Minor";

// Comma operator (returns last value)
let x = (1, 2, 3);   // x = 3

// in operator
"name" in { name: "Haseeb" }   // true
0 in [1, 2, 3]                  // true (checks index)

// instanceof
[] instanceof Array    // true
[] instanceof Object   // true (arrays are objects)

// Bitwise (less common in interviews but good to know)
&, |, ^, ~, <<, >>    // AND, OR, XOR, NOT, left shift, right shift
```

---

## Control Flow

```javascript
// if / else if / else
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else {
  grade = "F";
}

// switch
switch (day) {
  case "Monday":
  case "Tuesday":
    console.log("Weekday");
    break;
  case "Saturday":
  case "Sunday":
    console.log("Weekend");
    break;
  default:
    console.log("Unknown");
}

// for
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;  // skip
  if (i === 4) break;     // stop
  console.log(i);         // 0, 1, 3
}

// for...of (iterables: arrays, strings, maps, sets)
for (const item of [1, 2, 3]) { console.log(item); }
for (const char of "hello") { console.log(char); }

// for...in (object keys — avoid on arrays)
for (const key in { a: 1, b: 2 }) { console.log(key); }

// while
while (condition) { }

// do...while (runs at least once)
do { } while (condition);

// Labeled statements
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (j === 1) break outer; // breaks the outer loop
  }
}

// try / catch / finally
try {
  JSON.parse("invalid");
} catch (err) {
  console.log(err.message);
} finally {
  console.log("always runs");
}
```

---

## Functions

### Function Types

```javascript
// 1. Function Declaration (hoisted completely)
function greet(name) {
  return `Hello, ${name}!`;
}

// 2. Function Expression (not hoisted)
const greet = function(name) {
  return `Hello, ${name}!`;
};

// 3. Arrow Function (no own this, arguments, super, new.target)
const greet = (name) => `Hello, ${name}!`;
const square = n => n * n;
const add = (a, b) => a + b;
const getObj = () => ({ id: 1 }); // wrap object in parens

// 4. IIFE (Immediately Invoked Function Expression)
(function() {
  console.log("Runs immediately");
})();

((name) => {
  console.log(`Hi ${name}`);
})("Haseeb");

// 5. Named Function Expression
const factorial = function fact(n) {
  return n <= 1 ? 1 : n * fact(n - 1); // can reference itself
};

// 6. Generator Function
function* range(start, end) {
  for (let i = start; i <= end; i++) yield i;
}

// 7. Async Function
async function fetchData() {
  const res = await fetch("/api/data");
  return res.json();
}
```

### Parameters and Arguments

```javascript
// Default parameters
function createUser(name, role = "user", active = true) {
  return { name, role, active };
}

// Rest parameters (must be last)
function sum(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3, 4, 5); // 15

// Arguments object (available in regular functions, NOT arrow functions)
function logArgs() {
  console.log(arguments);        // array-like object
  console.log([...arguments]);   // convert to real array
}

// Higher-order functions
function multiply(factor) {
  return (number) => number * factor;   // returns a function
}
const double = multiply(2);
double(5);   // 10
double(10);  // 20

// Pure function (same input always same output, no side effects)
const add = (a, b) => a + b;

// Impure function (modifies external state)
let total = 0;
function addToTotal(n) { total += n; }
```

### Function Methods: call, apply, bind

```javascript
function greet(greeting, punctuation) {
  return `${greeting}, ${this.name}${punctuation}`;
}

const user = { name: "Haseeb" };

// call: invokes with explicit this, args passed individually
greet.call(user, "Hello", "!");     // "Hello, Haseeb!"

// apply: invokes with explicit this, args passed as array
greet.apply(user, ["Hi", "."]);     // "Hi, Haseeb."

// bind: returns a NEW function with this permanently bound
const greetHaseeb = greet.bind(user, "Hey");
greetHaseeb("?");                   // "Hey, Haseeb?"
greetHaseeb("!");                   // "Hey, Haseeb!"
```

---

## Scope and Closures

### Scope

```javascript
// Global scope
let globalVar = "I am global";

function outer() {
  // Function scope
  let outerVar = "I am outer";

  function inner() {
    // Function scope
    let innerVar = "I am inner";
    console.log(globalVar);  // accessible
    console.log(outerVar);   // accessible (via scope chain)
    console.log(innerVar);   // accessible
  }

  // console.log(innerVar); // ReferenceError
}

// Block scope
{
  let blockVar = "only here";
  const alsoBlock = "also only here";
  var notBlock = "leaks out";
}
// blockVar: ReferenceError
// notBlock: accessible
```

### Closures

A closure is a function that **remembers and accesses variables from its outer scope** even after the outer function has returned.

```javascript
function makeCounter(initial = 0) {
  let count = initial;   // private variable

  return {
    increment() { return ++count; },
    decrement() { return --count; },
    reset()     { count = initial; },
    value()     { return count; }
  };
}

const counter = makeCounter(10);
counter.increment(); // 11
counter.increment(); // 12
counter.decrement(); // 11
counter.value();     // 11
// count is NOT accessible from outside — true encapsulation
```

```javascript
// Classic closure in loops (the problem)
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
  // Prints: 3, 3, 3 (all share the same var i)
}

// Fix 1: use let (block-scoped)
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
  // Prints: 0, 1, 2
}

// Fix 2: IIFE closure
for (var i = 0; i < 3; i++) {
  ((j) => {
    setTimeout(() => console.log(j), 1000);
  })(i);
  // Prints: 0, 1, 2
}
```

```javascript
// Practical closure: memoization
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

const expensiveCalc = memoize((n) => {
  console.log("Computing...");
  return n * n;
});

expensiveCalc(5);  // "Computing..." → 25
expensiveCalc(5);  // 25 (from cache, no log)
```

---

## Hoisting

Hoisting is JavaScript's behavior of moving declarations to the top of their scope before execution.

```javascript
// Function declarations are fully hoisted
console.log(greet("Haseeb")); // "Hello, Haseeb!" (works before definition)
function greet(name) {
  return `Hello, ${name}!`;
}

// var is hoisted but initialized as undefined
console.log(x); // undefined (not ReferenceError)
var x = 5;
console.log(x); // 5

// let and const are hoisted but NOT initialized (Temporal Dead Zone)
// console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;

// Function expressions are NOT hoisted (the variable is, but not the function)
// console.log(sayHi()); // TypeError: sayHi is not a function
var sayHi = function() { return "Hi"; };

// Class declarations are hoisted but NOT initialized (TDZ, like let)
// const obj = new MyClass(); // ReferenceError
class MyClass { }
```

### Temporal Dead Zone (TDZ)

The TDZ is the period between entering a scope where `let`/`const` is declared and the line where it is initialized. Accessing the variable in this zone throws a `ReferenceError`.

---

## The this Keyword

`this` refers to the **execution context** — who called the function.

```javascript
// 1. Global context: this = global object (window in browser, global in Node)
console.log(this); // window (in browser)

// 2. Regular function: this = caller (or undefined in strict mode)
function show() {
  console.log(this);
}
show();           // window / undefined (strict mode)

// 3. Method: this = the object before the dot
const user = {
  name: "Haseeb",
  greet() {
    console.log(this.name); // "Haseeb"
  }
};
user.greet();

// 4. Arrow function: no own this, inherits from enclosing scope
const timer = {
  seconds: 0,
  start() {
    setInterval(() => {
      this.seconds++;   // this = timer (inherited from start's this)
      console.log(this.seconds);
    }, 1000);
  }
};

// 5. Constructor: this = newly created instance
function Person(name) {
  this.name = name;
  this.greet = function() {
    return `Hi, I'm ${this.name}`;
  };
}
const person = new Person("Haseeb");

// 6. Class: this = instance
class Car {
  constructor(brand) { this.brand = brand; }
  describe() { return `This is a ${this.brand}`; }
}

// 7. Explicit binding with call, apply, bind
function greet() { return `Hello, ${this.name}`; }
greet.call({ name: "Haseeb" });    // "Hello, Haseeb"

// 8. Event listener: this = the element that fired the event
btn.addEventListener("click", function() {
  console.log(this); // the button element
});

// Arrow in event listener: this = outer scope (not the element)
btn.addEventListener("click", () => {
  console.log(this); // window (or whatever outer this is)
});
```

---

## Prototypes and Inheritance

Every JavaScript object has an internal link to another object called its **prototype**. When you access a property that does not exist on the object, JavaScript looks up the prototype chain.

```javascript
// Every function has a prototype property
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function() {
  return `${this.name} makes a sound.`;
};

Animal.prototype.toString = function() {
  return `Animal: ${this.name}`;
};

const dog = new Animal("Rex");
dog.speak();    // "Rex makes a sound."

// Prototype chain
Object.getPrototypeOf(dog) === Animal.prototype   // true
Object.getPrototypeOf(Animal.prototype) === Object.prototype  // true
Object.getPrototypeOf(Object.prototype) === null   // true (end of chain)

// Prototypal inheritance
function Dog(name, breed) {
  Animal.call(this, name);    // call parent constructor
  this.breed = breed;
}

Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  return `${this.name} barks!`;
};

const rex = new Dog("Rex", "German Shepherd");
rex.speak();  // "Rex makes a sound." (inherited)
rex.bark();   // "Rex barks!"

rex instanceof Dog    // true
rex instanceof Animal // true

// hasOwnProperty: check own vs inherited
rex.hasOwnProperty("name")  // true (own)
rex.hasOwnProperty("speak") // false (inherited from prototype)

// Object.create
const animalProto = {
  speak() { return `${this.name} makes a sound.`; }
};
const cat = Object.create(animalProto);
cat.name = "Whiskers";
cat.speak(); // "Whiskers makes a sound."
```

---

## Classes

ES6 classes are syntactic sugar over prototype-based inheritance.

```javascript
class Animal {
  // Private fields (ES2022)
  #health = 100;

  constructor(name, type) {
    this.name = name;
    this.type = type;
  }

  // Instance method
  speak() {
    return `${this.name} makes a sound.`;
  }

  // Static method (called on class, not instance)
  static create(name, type) {
    return new Animal(name, type);
  }

  // Getter
  get info() {
    return `${this.name} (${this.type})`;
  }

  // Setter
  set healthPoints(value) {
    if (value < 0) throw new Error("Health cannot be negative");
    this.#health = value;
  }

  get healthPoints() {
    return this.#health;
  }

  // Private method
  #log() {
    console.log(`[Animal] ${this.name}`);
  }

  toString() {
    return this.info;
  }
}

// Inheritance
class Dog extends Animal {
  constructor(name, breed) {
    super(name, "Dog");   // must call super before using this
    this.breed = breed;
  }

  speak() {
    return `${this.name} barks!`;    // override
  }

  describe() {
    return `${super.speak()} I am a ${this.breed}.`; // call parent method
  }
}

const rex = new Dog("Rex", "Husky");
rex.speak();           // "Rex barks!"
rex.describe();        // "Rex barks! I am a Husky."
rex.info;              // "Rex (Dog)" (inherited getter)
rex.healthPoints = 80; // setter
rex.healthPoints;      // 80

// Mixins (multiple inheritance pattern)
const Serializable = (Base) => class extends Base {
  serialize() { return JSON.stringify(this); }
  static deserialize(data) { return Object.assign(new this(), JSON.parse(data)); }
};

class SerializableDog extends Serializable(Dog) {}
const d = new SerializableDog("Buddy", "Lab");
d.serialize(); // '{"name":"Buddy","type":"Dog","breed":"Lab"}'
```

---

## Arrays and Array Methods

```javascript
// Creation
const arr = [1, 2, 3];
const arr2 = new Array(3);          // [empty x 3]
const arr3 = Array.from("hello");   // ['h','e','l','l','o']
const arr4 = Array.from({length: 5}, (_, i) => i + 1); // [1,2,3,4,5]
const arr5 = Array.of(1, 2, 3);    // [1,2,3]

// Mutating methods (change original)
arr.push(4);            // adds to end, returns new length
arr.pop();              // removes from end, returns removed item
arr.unshift(0);         // adds to beginning, returns new length
arr.shift();            // removes from beginning, returns removed item
arr.splice(1, 2, "a"); // removes 2 elements at index 1, inserts "a"
arr.reverse();          // reverses in place
arr.sort();             // sorts in place (alphabetically by default!)
arr.sort((a, b) => a - b);  // numeric sort ascending
arr.sort((a, b) => b - a);  // numeric sort descending
arr.fill(0, 2, 4);     // fill with 0 from index 2 to 4
arr.copyWithin(0, 3);  // copy elements within array

// Non-mutating methods (return new array)
arr.map(x => x * 2);
arr.filter(x => x > 2);
arr.reduce((acc, x) => acc + x, 0);
arr.reduceRight((acc, x) => acc + x, 0);
arr.find(x => x > 2);          // first match or undefined
arr.findIndex(x => x > 2);     // first match index or -1
arr.findLast(x => x > 2);      // last match (ES2023)
arr.findLastIndex(x => x > 2); // last match index (ES2023)
arr.some(x => x > 2);          // true if any match
arr.every(x => x > 0);         // true if all match
arr.includes(2);                // true/false
arr.indexOf(2);                 // first index of 2, or -1
arr.lastIndexOf(2);             // last index of 2
arr.flat();                     // flattens one level
arr.flat(Infinity);             // flatten deeply
arr.flatMap(x => [x, x * 2]);  // map then flat one level
arr.slice(1, 3);                // returns new array [index1, index3)
arr.concat([4, 5]);             // joins arrays
arr.join(" - ");                // joins to string
arr.at(-1);                     // last element (ES2022)
arr.toReversed();               // reversed copy, no mutation (ES2023)
arr.toSorted((a,b) => a-b);    // sorted copy, no mutation (ES2023)
arr.toSpliced(1, 1, "x");      // spliced copy, no mutation (ES2023)
arr.with(2, "x");              // copy with index replaced (ES2023)

// Iteration
arr.forEach((item, index, array) => { });
for (const item of arr) { }
for (const [index, item] of arr.entries()) { }

// Conversion
arr.toString();    // "1,2,3"
arr.join(", ");    // "1, 2, 3"
[...arr];          // spread into new array

// Checking
Array.isArray(arr);         // true
arr.length;                 // 3
```

### Map, Filter, Reduce Deep Dive

```javascript
const users = [
  { id: 1, name: "Haseeb", age: 23, active: true },
  { id: 2, name: "Ahmed",  age: 17, active: false },
  { id: 3, name: "Sara",   age: 30, active: true }
];

// map: transform each element
const names = users.map(u => u.name);
// ["Haseeb", "Ahmed", "Sara"]

// filter: keep elements matching condition
const adults = users.filter(u => u.age >= 18);
// [{id:1,...}, {id:3,...}]

// reduce: accumulate into a single value
const totalAge = users.reduce((sum, u) => sum + u.age, 0);
// 70

// Chain them
const activeAdultNames = users
  .filter(u => u.active && u.age >= 18)
  .map(u => u.name);
// ["Haseeb", "Sara"]

// reduce to object (grouping)
const byId = users.reduce((acc, u) => {
  acc[u.id] = u;
  return acc;
}, {});
// { 1: {...}, 2: {...}, 3: {...} }
```

---

## Objects

```javascript
// Creation
const obj1 = { name: "Haseeb", age: 23 };
const obj2 = new Object();
const obj3 = Object.create(null);    // no prototype at all

// Shorthand properties
const name = "Haseeb";
const age = 23;
const user = { name, age };    // same as { name: name, age: age }

// Computed property names
const key = "role";
const config = { [key]: "admin", [`is_${key}`]: true };
// { role: "admin", is_role: true }

// Methods shorthand
const obj = {
  greet() { return "Hello"; },        // shorthand
  greet: function() { return "Hello"; } // equivalent
};

// Property access
obj.name;
obj["name"];    // useful for dynamic keys
obj?.missing;   // optional chaining, undefined instead of error

// Checking properties
"name" in obj;                   // true (includes prototype)
obj.hasOwnProperty("name");      // true (own properties only)
Object.hasOwn(obj, "name");      // true (modern, ES2022)

// Object methods
Object.keys(obj);                // array of own enumerable keys
Object.values(obj);              // array of own enumerable values
Object.entries(obj);             // array of [key, value] pairs
Object.fromEntries(entries);     // create object from entries

Object.assign({}, obj1, obj2);   // shallow merge (mutates target)
Object.freeze(obj);              // prevent all modifications
Object.seal(obj);                // allow modify, prevent add/delete
Object.isFrozen(obj);            // check if frozen

// Property descriptors
Object.defineProperty(obj, "id", {
  value: 42,
  writable: false,
  enumerable: false,
  configurable: false
});

Object.getOwnPropertyDescriptor(obj, "id");
Object.getOwnPropertyNames(obj);   // includes non-enumerable
Object.getOwnPropertySymbols(obj); // only Symbol keys

// Prototype
Object.getPrototypeOf(obj);
Object.setPrototypeOf(obj, proto);

// Shallow copy
const copy1 = { ...obj };
const copy2 = Object.assign({}, obj);

// Deep copy (modern)
const deep = structuredClone(obj);

// Merge
const merged = { ...defaults, ...overrides };
```

---

## Destructuring

```javascript
// Array destructuring
const [a, b, c] = [1, 2, 3];
const [first, , third] = [1, 2, 3];    // skip elements
const [x = 10, y = 20] = [5];          // defaults: x=5, y=20
const [head, ...tail] = [1, 2, 3, 4];  // rest: tail=[2,3,4]

// Swap variables
let p = 1, q = 2;
[p, q] = [q, p];    // p=2, q=1

// Object destructuring
const { name, age } = user;
const { name: userName, age: userAge } = user; // rename
const { role = "user", active = true } = user; // defaults
const { address: { city } } = user;            // nested

// Mixed
const { data: [firstItem, ...rest], status } = response;

// In function parameters
function display({ name, age = 0, role = "user" }) {
  return `${name}, ${age}, ${role}`;
}
display({ name: "Haseeb", age: 23 });
```

---

## Spread and Rest

```javascript
// Spread: expand iterable into individual elements
const arr = [1, 2, 3];
const arr2 = [...arr, 4, 5];       // [1,2,3,4,5]
const copy = [...arr];              // shallow copy
const merged = [...arr1, ...arr2];

Math.max(...arr);                   // spread into function args

// Spread with objects
const obj = { a: 1, b: 2 };
const extended = { ...obj, c: 3 };  // { a:1, b:2, c:3 }
const overridden = { ...obj, b: 99 }; // { a:1, b:99 }

// Rest: collect remaining into array (must be last)
function sum(first, second, ...others) {
  return first + second + others.reduce((a, b) => a + b, 0);
}

// Rest in destructuring
const [head, ...tail] = [1, 2, 3, 4];
const { a, b, ...remaining } = { a: 1, b: 2, c: 3, d: 4 };
// remaining = { c: 3, d: 4 }
```

---

## Iterables and Iterators

An **iterable** is any object with a `[Symbol.iterator]()` method. An **iterator** is an object with a `next()` method that returns `{ value, done }`.

```javascript
// Built-in iterables: Array, String, Map, Set, NodeList, arguments

// Manual iterator
function makeRangeIterator(start, end) {
  let current = start;
  return {
    [Symbol.iterator]() { return this; },
    next() {
      if (current <= end) {
        return { value: current++, done: false };
      }
      return { value: undefined, done: true };
    }
  };
}

const range = makeRangeIterator(1, 5);
for (const n of range) { console.log(n); }  // 1 2 3 4 5
[...makeRangeIterator(1, 3)];               // [1, 2, 3]
```

---

## Generators

Generators are functions that can pause and resume execution, producing a sequence of values on demand.

```javascript
function* counter(start = 0) {
  while (true) {
    const reset = yield start++;
    if (reset) start = 0;
  }
}

const gen = counter(1);
gen.next();         // { value: 1, done: false }
gen.next();         // { value: 2, done: false }
gen.next(true);     // { value: 0, done: false } (reset!)

// Finite generator
function* fibonacci() {
  let [a, b] = [0, 1];
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

function take(gen, n) {
  const result = [];
  for (const val of gen) {
    result.push(val);
    if (result.length === n) break;
  }
  return result;
}

take(fibonacci(), 8); // [0, 1, 1, 2, 3, 5, 8, 13]

// yield* delegate to another iterable
function* concat(...iterables) {
  for (const iter of iterables) {
    yield* iter;
  }
}

[...concat([1, 2], [3, 4], [5])]; // [1, 2, 3, 4, 5]
```

---

## Symbols

Symbols are unique, immutable primitive values often used as property keys to avoid name collisions.

```javascript
const id = Symbol("id");
const id2 = Symbol("id");
id === id2;    // false — always unique

// As object keys (not enumerable in for...in or Object.keys)
const KEY = Symbol("key");
const obj = { [KEY]: "secret", name: "Haseeb" };
Object.keys(obj);         // ["name"]
Object.getOwnPropertySymbols(obj); // [Symbol(key)]

// Well-known symbols
class MyArray {
  static [Symbol.iterator]() { /* custom iteration */ }
  [Symbol.toPrimitive](hint) {
    if (hint === "number") return 42;
    if (hint === "string") return "MyArray";
    return true;
  }
}

// Global symbol registry
const s1 = Symbol.for("shared");
const s2 = Symbol.for("shared");
s1 === s2;       // true (shared across realms)
Symbol.keyFor(s1); // "shared"
```

---

## Map, Set, WeakMap, WeakSet

```javascript
// Map: key-value pairs, any type as key, ordered by insertion
const map = new Map();
map.set("name", "Haseeb");
map.set(42, "answer");
map.set({}, "object key");

map.get("name");         // "Haseeb"
map.has("name");         // true
map.delete("name");      // true
map.size;                // number of entries
map.clear();             // removes all

// Map iteration
for (const [key, value] of map) { }
map.keys();
map.values();
map.entries();

// Initialize from array
const map2 = new Map([["a", 1], ["b", 2]]);

// Convert to object
Object.fromEntries(map);

// Set: unique values only, ordered by insertion
const set = new Set([1, 2, 3, 2, 1]);
set;          // Set(3) {1, 2, 3}
set.add(4);
set.has(2);   // true
set.delete(2);
set.size;     // 3

// Remove duplicates from array
const unique = [...new Set([1, 2, 2, 3, 3, 4])]; // [1,2,3,4]

// Set operations
const a = new Set([1, 2, 3, 4]);
const b = new Set([3, 4, 5, 6]);

// Union
const union = new Set([...a, ...b]);

// Intersection
const intersection = new Set([...a].filter(x => b.has(x)));

// Difference
const difference = new Set([...a].filter(x => !b.has(x)));

// WeakMap: keys must be objects, not enumerable, garbage collected
const cache = new WeakMap();
function processUser(user) {
  if (cache.has(user)) return cache.get(user);
  const result = expensiveOperation(user);
  cache.set(user, result);  // removed when user object is GC'd
  return result;
}

// WeakSet: stores objects only, not enumerable, garbage collected
const seen = new WeakSet();
function track(obj) {
  if (seen.has(obj)) return false;
  seen.add(obj);
  return true;
}
```

---

## Error Handling

```javascript
// Built-in error types
new Error("generic");
new TypeError("wrong type");
new ReferenceError("not defined");
new SyntaxError("invalid syntax");
new RangeError("out of range");
new URIError("invalid URI");
new EvalError("eval error");

// Custom error
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
    // Fix stack trace in V8
    if (Error.captureStackTrace) {
      Error.captureStackTrace(this, ValidationError);
    }
  }
}

// try / catch / finally
function parseJSON(str) {
  try {
    return { data: JSON.parse(str), error: null };
  } catch (err) {
    if (err instanceof SyntaxError) {
      return { data: null, error: "Invalid JSON" };
    }
    throw err;  // re-throw unexpected errors
  } finally {
    console.log("parseJSON completed");  // always runs
  }
}

// Error properties
const err = new Error("oops");
err.message;   // "oops"
err.name;      // "Error"
err.stack;     // stack trace string

// Async error handling
async function fetchUser(id) {
  try {
    const res = await fetch(`/api/users/${id}`);
    if (!res.ok) throw new Error(`HTTP error: ${res.status}`);
    return await res.json();
  } catch (err) {
    console.error("Failed to fetch user:", err);
    throw err;
  }
}
```

---

## Asynchronous JavaScript

JavaScript is single-threaded but handles async operations via the **event loop**.

### Callbacks

```javascript
// The original async pattern (leads to callback hell)
function loadUser(id, callback) {
  setTimeout(() => {
    callback(null, { id, name: "Haseeb" });
  }, 1000);
}

loadUser(1, (err, user) => {
  if (err) return console.error(err);
  loadPosts(user.id, (err, posts) => {  // callback hell
    if (err) return console.error(err);
    loadComments(posts[0].id, (err, comments) => {
      // pyramid of doom
    });
  });
});
```

---

## Promises

A Promise represents a value that may be available now, in the future, or never.

```javascript
// States: pending, fulfilled, rejected

// Creating a promise
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = Math.random() > 0.5;
    if (success) resolve({ data: "success" });
    else reject(new Error("something failed"));
  }, 1000);
});

// Consuming
promise
  .then(data => { console.log(data); return data; })  // on fulfilled
  .catch(err => { console.error(err); })               // on rejected
  .finally(() => { console.log("done"); });            // always

// Chaining
fetchUser(1)
  .then(user => fetchPosts(user.id))    // return value passed to next then
  .then(posts => fetchComments(posts[0].id))
  .then(comments => render(comments))
  .catch(err => handleError(err));      // catches ANY error in the chain

// Promise methods
Promise.resolve(value);       // already fulfilled
Promise.reject(error);        // already rejected

Promise.all([p1, p2, p3]);
// Waits for ALL to fulfill. Rejects immediately if ANY rejects.
// Returns array of results in same order.

Promise.allSettled([p1, p2, p3]);
// Waits for ALL to settle (fulfill or reject).
// Returns array of { status: "fulfilled"|"rejected", value|reason }

Promise.race([p1, p2, p3]);
// Settles as soon as the FIRST one settles (either way).

Promise.any([p1, p2, p3]);
// Fulfills as soon as the FIRST one fulfills.
// Rejects only if ALL reject (AggregateError).

// Promisify a callback function
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function withTimeout(promise, ms) {
  return Promise.race([
    promise,
    delay(ms).then(() => { throw new Error("Timeout"); })
  ]);
}
```

---

## Async and Await

`async/await` is syntactic sugar over Promises that makes async code look synchronous.

```javascript
// async function always returns a Promise
async function fetchUser(id) {
  const response = await fetch(`/api/users/${id}`);
  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }
  const user = await response.json();
  return user;
}

// Error handling
async function loadData() {
  try {
    const user = await fetchUser(1);
    const posts = await fetchPosts(user.id);    // sequential
    return { user, posts };
  } catch (err) {
    console.error("Failed:", err.message);
    return null;
  }
}

// Parallel execution (do not await sequentially when independent)
async function loadAll() {
  // Sequential (slower — waits for each before starting next)
  const user  = await fetchUser(1);
  const posts = await fetchPosts(1);

  // Parallel (faster — both start at the same time)
  const [user2, posts2] = await Promise.all([
    fetchUser(1),
    fetchPosts(1)
  ]);
}

// for await...of (async iteration)
async function processStream(stream) {
  for await (const chunk of stream) {
    process(chunk);
  }
}

// Top-level await (in ES modules)
const config = await fetch("/config.json").then(r => r.json());
```

---

## Event Loop

The event loop is what allows JavaScript to perform non-blocking operations despite being single-threaded.

```
    ┌─────────────────────────┐
    │        Call Stack        │  ← synchronous code runs here
    └────────────┬────────────┘
                 │ empty?
    ┌────────────▼────────────┐
    │     Microtask Queue      │  ← Promises, queueMicrotask, MutationObserver
    │  (drained completely     │
    │   before moving on)      │
    └────────────┬────────────┘
                 │ empty?
    ┌────────────▼────────────┐
    │      Macrotask Queue     │  ← setTimeout, setInterval, I/O, UI events
    │  (one task at a time)    │
    └─────────────────────────┘
```

```javascript
console.log("1 - sync");

setTimeout(() => console.log("2 - macrotask"), 0);

Promise.resolve()
  .then(() => console.log("3 - microtask"))
  .then(() => console.log("4 - microtask 2"));

queueMicrotask(() => console.log("5 - microtask 3"));

console.log("6 - sync");

// Output order:
// 1 - sync
// 6 - sync
// 3 - microtask
// 4 - microtask 2
// 5 - microtask 3
// 2 - macrotask
```

> **Interview Tip:** Microtasks (Promises) always run before macrotasks (setTimeout). The microtask queue is completely drained after every task before the next macrotask is picked up. This is why a resolved Promise always runs before a `setTimeout` with 0ms delay.

---

## DOM Manipulation

```javascript
// Selecting elements
document.getElementById("id");
document.querySelector(".class");          // first match
document.querySelectorAll("div.card");     // NodeList of all matches
document.getElementsByClassName("card");   // live HTMLCollection
document.getElementsByTagName("div");

// Creating and inserting
const div = document.createElement("div");
div.textContent = "Hello";
div.innerHTML = "<span>Hello</span>";      // careful: XSS risk
div.setAttribute("class", "card");
div.classList.add("active");
div.classList.remove("hidden");
div.classList.toggle("open");
div.classList.contains("card");           // true
div.dataset.userId = "42";               // sets data-user-id attribute

// Insertion
parent.appendChild(div);
parent.prepend(div);
parent.append(div, "text", otherEl);
parent.insertBefore(div, referenceEl);
referenceEl.before(div);
referenceEl.after(div);
referenceEl.replaceWith(div);

// Removal
el.remove();
parent.removeChild(el);

// Navigation
el.parentElement;
el.children;             // live HTMLCollection of element children
el.childNodes;           // live NodeList including text nodes
el.firstElementChild;
el.lastElementChild;
el.nextElementSibling;
el.previousElementSibling;
el.closest(".parent");   // walks up the DOM tree

// Dimensions and position
el.getBoundingClientRect();  // { top, left, right, bottom, width, height }
el.offsetWidth;
el.offsetHeight;
el.scrollTop;
el.scrollLeft;
window.scrollY;
window.scrollX;
el.scrollIntoView({ behavior: "smooth", block: "start" });

// Style
el.style.color = "red";
el.style.cssText = "color: red; font-size: 16px;";
getComputedStyle(el).color;    // read computed styles

// Document fragment (batch DOM updates)
const fragment = document.createDocumentFragment();
items.forEach(item => {
  const li = document.createElement("li");
  li.textContent = item;
  fragment.appendChild(li);
});
ul.appendChild(fragment); // single DOM update
```

---

## Events and Event Delegation

```javascript
// Adding event listeners
element.addEventListener("click", handler);
element.addEventListener("click", handler, { once: true });   // fires once
element.addEventListener("click", handler, { capture: true }); // capture phase
element.addEventListener("click", handler, { passive: true }); // never calls preventDefault (scroll perf)

// Removing
element.removeEventListener("click", handler); // same function reference required

// Event object
function handler(event) {
  event.target;             // element that triggered the event
  event.currentTarget;      // element the listener is on
  event.type;               // "click"
  event.preventDefault();   // stop default browser behavior
  event.stopPropagation();  // stop bubbling up
  event.stopImmediatePropagation(); // stop other listeners on same element
  event.bubbles;            // does this event bubble?
  event.key;                // keyboard key
  event.clientX;            // mouse X position
  event.clientY;            // mouse Y position
}

// Event phases: Capture → Target → Bubble

// Event delegation (single listener for many children)
// Instead of adding listener to each list item:
ul.addEventListener("click", (event) => {
  const li = event.target.closest("li");  // find the li that was clicked
  if (!li) return;
  console.log("Clicked:", li.dataset.id);
});

// Custom events
const customEvent = new CustomEvent("userLoggedIn", {
  detail: { userId: 42, role: "admin" },
  bubbles: true,
  cancelable: true
});
document.dispatchEvent(customEvent);
document.addEventListener("userLoggedIn", (e) => {
  console.log(e.detail.userId);
});

// Common events
// Mouse: click, dblclick, mousedown, mouseup, mousemove, mouseenter, mouseleave, mouseover, mouseout, contextmenu
// Keyboard: keydown, keyup, keypress (deprecated)
// Form: submit, change, input, focus, blur, reset, focusin, focusout
// Window: load, DOMContentLoaded, resize, scroll, beforeunload, unload
// Touch: touchstart, touchend, touchmove
// Drag: dragstart, drag, dragend, dragenter, dragleave, dragover, drop
```

---

## Fetch API and HTTP

```javascript
// Basic GET
const res = await fetch("https://api.example.com/users");
const data = await res.json();

// Full request
const response = await fetch("https://api.example.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": `Bearer ${token}`
  },
  body: JSON.stringify({ name: "Haseeb", role: "dev" }),
  credentials: "include",   // send cookies cross-origin
  cache: "no-cache",
  signal: AbortController.signal   // for cancellation
});

if (!response.ok) {
  throw new Error(`HTTP error! status: ${response.status}`);
}

// Response methods
response.json();     // parse JSON body
response.text();     // raw text body
response.blob();     // binary data
response.formData();
response.arrayBuffer();

// Response properties
response.status;     // 200, 404, etc.
response.statusText; // "OK", "Not Found"
response.ok;         // true if status 200-299
response.headers.get("Content-Type");
response.url;

// Abort / cancel request
const controller = new AbortController();
const timeout = setTimeout(() => controller.abort(), 5000);

try {
  const res = await fetch("/api/data", { signal: controller.signal });
  const data = await res.json();
  clearTimeout(timeout);
  return data;
} catch (err) {
  if (err.name === "AbortError") {
    console.log("Request timed out");
  }
}

// Reusable fetch wrapper
async function api(endpoint, options = {}) {
  const baseURL = "https://api.example.com";
  const defaultHeaders = {
    "Content-Type": "application/json",
    "Authorization": `Bearer ${localStorage.getItem("token")}`
  };

  const res = await fetch(`${baseURL}${endpoint}`, {
    ...options,
    headers: { ...defaultHeaders, ...options.headers }
  });

  if (!res.ok) {
    const error = await res.json().catch(() => ({}));
    throw Object.assign(new Error(error.message || "API Error"), {
      status: res.status,
      data: error
    });
  }

  return res.json();
}
```

---

## Modules

```javascript
// Named exports
export const PI = 3.14159;
export function add(a, b) { return a + b; }
export class Calculator { }

// Default export (one per file)
export default function main() { }

// Named imports
import { PI, add } from "./math.js";
import { add as sum } from "./math.js";  // rename

// Default import
import main from "./main.js";

// Import all
import * as Math from "./math.js";
Math.PI;
Math.add(1, 2);

// Import default and named together
import React, { useState, useEffect } from "react";

// Re-export
export { add } from "./math.js";
export { default as main } from "./main.js";
export * from "./utils.js";

// Dynamic import (lazy loading)
const { default: Chart } = await import("./chart.js");

// Conditional import
if (condition) {
  const module = await import("./heavy-module.js");
}

// In HTML
<script type="module" src="main.js"></script>

// Differences from CommonJS (Node.js)
// ESM                          CJS
// import / export              require / module.exports
// Static analysis              Dynamic
// async loading                sync loading
// strict mode by default       not by default
// .mjs or type: "module"       .js default
```

---

## Design Patterns

### Singleton

```javascript
class DatabaseConnection {
  static #instance = null;

  constructor(url) {
    if (DatabaseConnection.#instance) {
      return DatabaseConnection.#instance;
    }
    this.url = url;
    this.connection = this.#connect();
    DatabaseConnection.#instance = this;
  }

  #connect() { /* ... */ }

  static getInstance(url) {
    if (!DatabaseConnection.#instance) {
      new DatabaseConnection(url);
    }
    return DatabaseConnection.#instance;
  }
}
```

### Observer / Event Emitter

```javascript
class EventEmitter {
  #events = {};

  on(event, listener) {
    (this.#events[event] ||= []).push(listener);
    return () => this.off(event, listener); // unsubscribe fn
  }

  off(event, listener) {
    this.#events[event] = (this.#events[event] || [])
      .filter(l => l !== listener);
  }

  emit(event, ...args) {
    (this.#events[event] || []).forEach(l => l(...args));
  }

  once(event, listener) {
    const wrapper = (...args) => {
      listener(...args);
      this.off(event, wrapper);
    };
    this.on(event, wrapper);
  }
}
```

### Factory

```javascript
function createUser(type, data) {
  const base = { ...data, createdAt: new Date() };

  const types = {
    admin:   () => ({ ...base, role: "admin",   permissions: ["read","write","delete"] }),
    editor:  () => ({ ...base, role: "editor",  permissions: ["read","write"] }),
    viewer:  () => ({ ...base, role: "viewer",  permissions: ["read"] })
  };

  if (!types[type]) throw new Error(`Unknown user type: ${type}`);
  return types[type]();
}
```

### Module Pattern

```javascript
const ShoppingCart = (() => {
  let items = [];  // private

  return {
    add(item) { items.push(item); },
    remove(id) { items = items.filter(i => i.id !== id); },
    getItems() { return [...items]; },  // return copy, not reference
    total() { return items.reduce((sum, i) => sum + i.price, 0); },
    clear() { items = []; }
  };
})();
```

### Decorator (using higher-order functions)

```javascript
function withLogging(fn) {
  return function(...args) {
    console.log(`Calling ${fn.name} with`, args);
    const result = fn.apply(this, args);
    console.log(`${fn.name} returned`, result);
    return result;
  };
}

function withRetry(fn, retries = 3) {
  return async function(...args) {
    for (let i = 0; i <= retries; i++) {
      try {
        return await fn.apply(this, args);
      } catch (err) {
        if (i === retries) throw err;
        await delay(1000 * 2 ** i);  // exponential backoff
      }
    }
  };
}
```

---

## Functional Programming Concepts

```javascript
// 1. Pure functions (same input, same output, no side effects)
const add = (a, b) => a + b;
const double = arr => arr.map(x => x * 2);  // returns new array

// 2. Immutability
const original = { name: "Haseeb", skills: ["JS", "React"] };
const updated = {
  ...original,
  skills: [...original.skills, "Python"]
};

// 3. Function composition
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);
const pipe    = (...fns) => x => fns.reduce((v, f) => f(v), x);

const process = pipe(
  str => str.trim(),
  str => str.toLowerCase(),
  str => str.replace(/\s+/g, "-")
);
process("  Hello World  "); // "hello-world"

// 4. Currying
const curry = fn => {
  const arity = fn.length;
  return function curried(...args) {
    if (args.length >= arity) return fn(...args);
    return (...more) => curried(...args, ...more);
  };
};

const add3 = curry((a, b, c) => a + b + c);
add3(1)(2)(3);   // 6
add3(1, 2)(3);   // 6
add3(1)(2, 3);   // 6

// 5. Partial application
const multiply = (factor, number) => factor * number;
const triple = multiply.bind(null, 3);
triple(5);   // 15

// 6. Functor (mappable)
const Box = value => ({
  map: fn => Box(fn(value)),
  fold: fn => fn(value)
});

Box(5)
  .map(x => x * 2)
  .map(x => x + 1)
  .fold(x => console.log(x)); // 11
```

---

## Memory Management and Garbage Collection

JavaScript uses **automatic garbage collection** with a **mark-and-sweep** algorithm.

```javascript
// Memory leaks to watch for:

// 1. Forgotten timers / intervals
const id = setInterval(() => {
  doSomething(bigData);
}, 1000);
// Always clear when done
clearInterval(id);

// 2. Event listeners not removed
function setup() {
  const handler = () => console.log("clicked");
  element.addEventListener("click", handler);

  // Return cleanup function
  return () => element.removeEventListener("click", handler);
}

// 3. Closures holding large objects
function createHeavy() {
  const bigArray = new Array(1000000).fill("*");
  return () => bigArray.length;  // holds reference to bigArray
}

// 4. Detached DOM nodes
let detachedNode;
function detach() {
  const node = document.getElementById("panel");
  detachedNode = node;        // global reference!
  node.parentNode.removeChild(node);
}
// Fix: detachedNode = null when done

// 5. Circular references (modern GC handles this, but still bad practice)
const obj = {};
obj.self = obj;   // circular reference

// WeakRef (hold reference without preventing GC)
const ref = new WeakRef(target);
const obj = ref.deref();  // undefined if GC'd
if (obj) { /* use obj */ }

// FinalizationRegistry (run callback when object is GC'd)
const registry = new FinalizationRegistry((key) => {
  cache.delete(key);
});
registry.register(target, cacheKey);
```

---

## Performance Best Practices

```javascript
// 1. Debounce (delay execution until after user stops triggering)
function debounce(fn, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
const debouncedSearch = debounce(search, 300);
input.addEventListener("input", debouncedSearch);

// 2. Throttle (execute at most once per interval)
function throttle(fn, limit) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      return fn.apply(this, args);
    }
  };
}
const throttledScroll = throttle(handleScroll, 100);
window.addEventListener("scroll", throttledScroll);

// 3. Memoization (cache expensive results)
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

// 4. Lazy evaluation
const heavyResult = condition ? computeHeavy() : null;  // eager
const getResult = () => condition ? computeHeavy() : null;  // lazy

// 5. Avoid layout thrashing (read all, then write all)
// Bad: interleaves reads and writes, forces multiple reflows
elements.forEach(el => {
  const h = el.offsetHeight;  // read (forces reflow)
  el.style.height = h * 2 + "px";  // write (invalidates layout)
});

// Good: batch reads, then batch writes
const heights = elements.map(el => el.offsetHeight);  // all reads
elements.forEach((el, i) => {
  el.style.height = heights[i] * 2 + "px";  // all writes
});

// 6. Use requestAnimationFrame for visual updates
function animate() {
  update();
  draw();
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);

// 7. Web Workers for CPU-intensive tasks
const worker = new Worker("worker.js");
worker.postMessage({ data: largeArray });
worker.onmessage = (e) => console.log("Result:", e.data);
// worker.js: self.onmessage = e => self.postMessage(process(e.data));

// 8. Use appropriate data structures
// O(1) lookup: Object or Map (not Array.find which is O(n))
const userMap = new Map(users.map(u => [u.id, u]));
userMap.get(42);  // O(1)
```

---

## Common Interview Questions

### Q1. What is the difference between `==` and `===`?
`==` performs type coercion before comparison, which can lead to surprising results like `0 == false` being `true`. `===` checks both value and type with no coercion. Always use `===` unless you have a specific reason to use `==`.

### Q2. What is a closure?
A closure is a function that retains access to its outer scope's variables even after the outer function has returned. This happens because functions in JavaScript capture a reference to their surrounding lexical environment, not a copy of it.

### Q3. What is the difference between `var`, `let`, and `const`?
`var` is function-scoped and hoisted (initialized to `undefined`). `let` and `const` are block-scoped and hoisted but in the Temporal Dead Zone (TDZ) until their declaration line. `const` cannot be reassigned after declaration, but objects and arrays it holds can still be mutated.

### Q4. Explain how the event loop works.
JavaScript runs on a single thread with a call stack. When async operations (timers, network requests) complete, their callbacks are placed in queues. The event loop continuously checks if the call stack is empty, then processes the microtask queue completely (Promises, queueMicrotask), then picks one task from the macrotask queue (setTimeout, setInterval), and repeats.

### Q5. What is the difference between `null` and `undefined`?
`undefined` means a variable has been declared but not yet assigned a value. `null` is an intentional assignment meaning "no value". `typeof null` returns `"object"` which is a historical JavaScript bug. Use `=== null` to check for null specifically.

### Q6. What is prototypal inheritance?
Every JavaScript object has a prototype — an internal link to another object. When you access a property that does not exist on an object, the engine walks up the prototype chain until it finds the property or reaches `null`. ES6 classes are syntactic sugar over this prototype chain mechanism.

### Q7. What is `this` in JavaScript?
`this` refers to the execution context of the function. In a regular function, it is determined by how the function is called (the object before the dot). Arrow functions do not have their own `this` and inherit it from the enclosing lexical scope. You can explicitly set `this` with `call`, `apply`, or `bind`.

### Q8. What is the difference between `Promise.all` and `Promise.allSettled`?
`Promise.all` rejects immediately if any promise rejects, giving you the first error but losing results from others. `Promise.allSettled` waits for all promises to settle regardless of outcome and gives you an array of results with status for each, making it useful when you need all results even if some failed.

### Q9. What is event delegation?
Event delegation is a pattern where you add a single event listener to a parent element instead of multiple listeners on child elements. Because events bubble up the DOM, the parent's listener catches events from all descendants. You then use `event.target` to identify which child triggered the event. This is more efficient and works for dynamically added children.

### Q10. What is the difference between deep and shallow copy?
A shallow copy duplicates the top-level structure but nested objects still share the same reference. A deep copy creates entirely new objects at all levels. `{...obj}` and `Object.assign` are shallow. `structuredClone(obj)` is the modern deep copy method. `JSON.parse(JSON.stringify(obj))` is a quick deep copy but loses functions, Dates, `undefined`, and special values.

### Q11. What is a debounce vs throttle?
Both limit how often a function runs. Debounce delays execution until a specified time has passed since the last call (useful for search inputs). Throttle ensures a function runs at most once per interval regardless of how many times it is triggered (useful for scroll or resize events).

### Q12. What is hoisting?
Hoisting is the behavior where variable and function declarations are conceptually moved to the top of their scope before execution. Function declarations are fully hoisted. `var` is hoisted but initialized as `undefined`. `let` and `const` are hoisted but live in the Temporal Dead Zone and throw a `ReferenceError` if accessed before their declaration.

### Q13. What is the difference between `call`, `apply`, and `bind`?
All three let you set the `this` value for a function. `call` invokes the function immediately with arguments passed individually. `apply` invokes immediately with arguments as an array. `bind` returns a new function permanently bound to the given `this`, which you can call later.

### Q14. What is a generator function?
A generator is a function declared with `function*` that can pause execution with `yield` and resume later. Calling a generator returns an iterator that you advance with `.next()`. Each call to `.next()` runs the function until the next `yield` and returns `{ value, done }`. Generators are useful for lazy evaluation, infinite sequences, and implementing async flows.

### Q15. What is the Temporal Dead Zone?
The TDZ is the period between entering a block scope where a `let` or `const` is declared and the actual line of that declaration. During this zone, the variable exists in memory but is not initialized, so accessing it throws a `ReferenceError`. This is why `let` and `const` appear "not hoisted" even though they technically are.

---

## Contributing

Found an issue or want to add a topic? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).