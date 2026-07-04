# 🔷 TypeScript Interview Essentials

> A complete, beginner-friendly reference guide covering every TypeScript concept you need to ace frontend and full-stack developer interviews. Written in simple, easy English with clear code examples and real-world patterns.

---

## 📌 Table of Contents

- [What is TypeScript?](#what-is-typescript)
- [Why Use TypeScript?](#why-use-typescript)
- [Basic Types](#basic-types)
- [Type Inference](#type-inference)
- [Arrays and Tuples](#arrays-and-tuples)
- [Objects and Type Aliases](#objects-and-type-aliases)
- [Interfaces](#interfaces)
- [Interface vs Type Alias](#interface-vs-type-alias)
- [Union and Intersection Types](#union-and-intersection-types)
- [Literal Types](#literal-types)
- [Functions in TypeScript](#functions-in-typescript)
- [Enums](#enums)
- [Type Assertions](#type-assertions)
- [Any, Unknown, Never, Void](#any-unknown-never-void)
- [Optional and Readonly Properties](#optional-and-readonly-properties)
- [Generics](#generics)
- [Classes in TypeScript](#classes-in-typescript)
- [Type Narrowing](#type-narrowing)
- [Utility Types](#utility-types)
- [Mapped Types](#mapped-types)
- [Conditional Types](#conditional-types)
- [keyof and typeof Operators](#keyof-and-typeof-operators)
- [Index Signatures](#index-signatures)
- [Modules and Namespaces](#modules-and-namespaces)
- [Declaration Files (.d.ts)](#declaration-files-dts)
- [TypeScript with React](#typescript-with-react)
- [tsconfig.json Explained](#tsconfigjson-explained)
- [Common Errors and How to Fix Them](#common-errors-and-how-to-fix-them)
- [Best Practices](#best-practices)
- [Common Interview Questions](#common-interview-questions)

---

## What is TypeScript?

TypeScript is **JavaScript with types added on top**. It was created by Microsoft. Every valid JavaScript file is also valid TypeScript — TypeScript just lets you add extra information (types) that helps catch mistakes before your code even runs.

Think of it like this: JavaScript is like writing without checking grammar. TypeScript is like having a grammar checker that tells you about mistakes while you type, before you even hit "publish".

```typescript
// Plain JavaScript — no warning, error happens at runtime
function add(a, b) {
  return a + b;
}
add("5", 10); // "510" — probably not what you wanted, but no error

// TypeScript — catches the mistake immediately while you write code
function add(a: number, b: number): number {
  return a + b;
}
add("5", 10); // Error: Argument of type 'string' is not assignable to parameter of type 'number'
```

TypeScript code is **compiled (transpiled)** into plain JavaScript before it runs in the browser or Node.js. The types only exist while you are writing code — they disappear completely after compilation.

---

## Why Use TypeScript?

- **Catches bugs early** — type errors show up while coding, not in production
- **Better autocomplete** — your editor knows exactly what properties and methods exist
- **Self-documenting code** — types describe what a function expects and returns
- **Easier refactoring** — change something and TypeScript shows you everywhere it breaks
- **Better team collaboration** — types act as a contract between different parts of code
- **Huge industry adoption** — most modern companies and frameworks (Next.js, Angular, NestJS) expect TypeScript

---

## Basic Types

```typescript
// Primitive types
let age: number = 23;
let name: string = "Haseeb";
let isActive: boolean = true;
let nothing: null = null;
let notDefined: undefined = undefined;
let bigNumber: bigint = 100n;
let id: symbol = Symbol("id");

// Type comes AFTER the variable name, separated by a colon
let score: number;
score = 95;
// score = "95"; // Error: Type 'string' is not assignable to type 'number'

// You can declare without assigning right away
let username: string;
username = "haseeb_dev";
```

---

## Type Inference

TypeScript is smart. If you assign a value right away, it automatically figures out the type for you — you do not always need to write it explicitly.

```typescript
// TypeScript infers the type automatically
let age = 23;          // inferred as: number
let name = "Haseeb";   // inferred as: string
let isStudent = true;  // inferred as: boolean

// age = "23"; // Error! TypeScript remembers age is a number

// You still need explicit types for function parameters
// (TypeScript cannot guess what you will pass in)
function greet(name: string) {
  return `Hello, ${name}`;
}

// Best practice: let TypeScript infer when possible, be explicit when it helps clarity
const numbers = [1, 2, 3];          // inferred as number[]
const user = { name: "Haseeb", age: 23 };  // inferred as { name: string; age: number }
```

> **Interview Tip:** A common best practice is "let TypeScript infer simple variable types, but always explicitly type function parameters and return types." This keeps code clean without sacrificing safety.

---

## Arrays and Tuples

```typescript
// Arrays — two equivalent syntaxes
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["Haseeb", "Ahmed"];

// Array of objects
let users: { name: string; age: number }[] = [
  { name: "Haseeb", age: 23 },
];

// Mixed type arrays using union
let mixed: (string | number)[] = [1, "two", 3];

// Readonly array (cannot push, pop, or modify)
let fixedNumbers: readonly number[] = [1, 2, 3];
// fixedNumbers.push(4); // Error: Property 'push' does not exist on type 'readonly number[]'

// Tuples — fixed length array where EACH position has its own type
let person: [string, number] = ["Haseeb", 23];
// person = [23, "Haseeb"]; // Error: order matters!

// Named tuples (for clarity)
let coordinate: [x: number, y: number] = [10, 20];

// Tuple with optional element
let response: [number, string?] = [200];

// Tuple with rest element
let scores: [string, ...number[]] = ["Haseeb", 90, 85, 95];

// Real-world tuple use case: React useState return type
function useToggle(): [boolean, () => void] {
  let value = false;
  const toggle = () => { value = !value; };
  return [value, toggle];
}
```

---

## Objects and Type Aliases

```typescript
// Inline object type
let user: { name: string; age: number; email: string } = {
  name: "Haseeb",
  age: 23,
  email: "contactimhaseeb@gmail.com",
};

// Type alias — gives a name to a type so you can reuse it
type User = {
  name: string;
  age: number;
  email: string;
};

let user1: User = { name: "Haseeb", age: 23, email: "h@test.com" };
let user2: User = { name: "Ahmed", age: 25, email: "a@test.com" };

// Nested object types
type Address = {
  street: string;
  city: string;
  zipCode: string;
};

type Customer = {
  name: string;
  address: Address;        // reuse the Address type
};

const customer: Customer = {
  name: "Haseeb",
  address: {
    street: "123 Main St",
    city: "Karachi",
    zipCode: "75500",
  },
};

// Type alias for primitives (less common but useful)
type ID = string | number;
type Status = "pending" | "active" | "completed";
```

---

## Interfaces

An interface is another way to describe the shape of an object. It is very similar to a type alias but with a few key differences (explained in the next section).

```typescript
interface User {
  name: string;
  age: number;
  email: string;
}

const user: User = {
  name: "Haseeb",
  age: 23,
  email: "contactimhaseeb@gmail.com",
};

// Extending interfaces (interface inheritance)
interface Animal {
  name: string;
  sound(): string;
}

interface Dog extends Animal {
  breed: string;
}

const myDog: Dog = {
  name: "Rex",
  breed: "Husky",
  sound: () => "Woof!",
};

// Extending multiple interfaces
interface Swimmer {
  swim(): void;
}
interface Flyer {
  fly(): void;
}
interface Duck extends Swimmer, Flyer {
  quack(): void;
}

// Function type with interface
interface AddFunction {
  (a: number, b: number): number;
}
const add: AddFunction = (a, b) => a + b;

// Interface with optional and readonly properties
interface Product {
  readonly id: string;     // can be set once, never changed after
  name: string;
  price: number;
  description?: string;    // optional, may or may not exist
}

const product: Product = {
  id: "prod-001",
  name: "Laptop",
  price: 999,
};
// product.id = "prod-002"; // Error: id is readonly

// Declaration merging (a unique interface feature, not available with type)
interface Window {
  myCustomProperty: string;
}
// This adds myCustomProperty to the existing global Window interface
```

---

## Interface vs Type Alias

This is one of the most commonly asked TypeScript interview questions.

```typescript
// Both can describe object shapes in basically the same way
interface UserInterface {
  name: string;
  age: number;
}

type UserType = {
  name: string;
  age: number;
};

// Interfaces can be extended with "extends"
interface Animal { name: string; }
interface Dog extends Animal { breed: string; }

// Type aliases use intersection (&) instead
type Animal = { name: string; };
type Dog = Animal & { breed: string; };

// ONLY interfaces support declaration merging
interface Car { brand: string; }
interface Car { model: string; }  // merges automatically!
// Now Car has both brand AND model

// ONLY type aliases can represent union types, primitives, or tuples directly
type Status = "active" | "inactive";  // union — interfaces cannot do this
type ID = string | number;             // primitive union
type Point = [number, number];         // tuple
```

| Feature | `interface` | `type` |
|---|---|---|
| Object shapes | Yes | Yes |
| Extends / inheritance | `extends` keyword | `&` intersection |
| Union types | No | Yes |
| Declaration merging | Yes (auto-merges) | No (causes an error if duplicated) |
| Primitives, tuples | No | Yes |
| Implements in classes | Yes | Yes |

> **Interview Tip:** A common, safe answer is: "Use `interface` for defining the shape of objects and classes, especially when you might need to extend them later. Use `type` for unions, primitives, tuples, or more complex type compositions." Both work for most everyday cases — this is mostly a team preference.

---

## Union and Intersection Types

```typescript
// Union (|): value can be ONE of several types
let id: string | number;
id = "abc123";    // valid
id = 42;           // valid
// id = true;      // Error

// Union with literal types
type Status = "pending" | "active" | "completed";
let orderStatus: Status = "pending";
// orderStatus = "cancelled"; // Error: not one of the allowed values

// Union in function parameters
function printId(id: string | number) {
  console.log(`ID: ${id}`);
}
printId(101);
printId("202");

// Intersection (&): combines MULTIPLE types into ONE (must have ALL properties)
type Person = {
  name: string;
  age: number;
};

type Employee = {
  employeeId: string;
  department: string;
};

type StaffMember = Person & Employee;  // must have ALL properties from both

const staff: StaffMember = {
  name: "Haseeb",
  age: 23,
  employeeId: "EMP-001",
  department: "Engineering",
};

// Real-world intersection example: combining base + specific props
type BaseProps = { className?: string; id?: string };
type ButtonProps = BaseProps & { onClick: () => void; label: string };
```

---

## Literal Types

```typescript
// String literal types — only specific exact values are allowed
let direction: "up" | "down" | "left" | "right";
direction = "up";    // valid
// direction = "north"; // Error: not one of the allowed values

// Number literal types
let diceRoll: 1 | 2 | 3 | 4 | 5 | 6;
diceRoll = 4;
// diceRoll = 7; // Error

// Boolean literal types
let isTrue: true;
isTrue = true;
// isTrue = false; // Error

// Combining literals with regular types (very common pattern for variants)
type ButtonVariant = "primary" | "secondary" | "danger" | "ghost";
type ButtonSize = "small" | "medium" | "large";

interface ButtonProps {
  variant: ButtonVariant;
  size: ButtonSize;
  label: string;
}

function Button({ variant, size, label }: ButtonProps) {
  // implementation
}

Button({ variant: "primary", size: "medium", label: "Submit" }); // valid
// Button({ variant: "warning", size: "medium", label: "Submit" }); // Error
```

---

## Functions in TypeScript

```typescript
// Basic function typing
function add(a: number, b: number): number {
  return a + b;
}

// Arrow function typing
const multiply = (a: number, b: number): number => a * b;

// Void return type (function returns nothing useful)
function logMessage(message: string): void {
  console.log(message);
}

// Optional parameters (must come after required ones)
function greet(name: string, greeting?: string): string {
  return `${greeting ?? "Hello"}, ${name}!`;
}
greet("Haseeb");                  // "Hello, Haseeb!"
greet("Haseeb", "Hi there");      // "Hi there, Haseeb!"

// Default parameters
function createUser(name: string, role: string = "user"): object {
  return { name, role };
}

// Rest parameters
function sum(...numbers: number[]): number {
  return numbers.reduce((total, n) => total + n, 0);
}
sum(1, 2, 3, 4); // 10

// Function type as a variable type
let calculate: (a: number, b: number) => number;
calculate = (a, b) => a + b;

// Function overloads (same function, different parameter combinations)
function getLength(value: string): number;
function getLength(value: any[]): number;
function getLength(value: string | any[]): number {
  return value.length;
}
getLength("hello");        // 5
getLength([1, 2, 3]);      // 3

// Functions as object properties
interface Calculator {
  add(a: number, b: number): number;
  subtract(a: number, b: number): number;
}

const calculator: Calculator = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b,
};
```

---

## Enums

Enums let you define a set of **named constants**. They make code more readable than using raw numbers or strings everywhere.

```typescript
// Numeric enum (default: starts at 0, auto-increments)
enum Direction {
  Up,      // 0
  Down,    // 1
  Left,    // 2
  Right,   // 3
}
let dir: Direction = Direction.Up;
console.log(dir); // 0

// Numeric enum with custom starting value
enum StatusCode {
  Success = 200,
  NotFound = 404,
  ServerError = 500,
}

// String enum (more readable, recommended over numeric)
enum Role {
  Admin = "ADMIN",
  Editor = "EDITOR",
  Viewer = "VIEWER",
}

function checkPermission(role: Role) {
  if (role === Role.Admin) {
    return "Full access";
  }
  return "Limited access";
}
checkPermission(Role.Admin);

// const enum (removed completely at compile time, more performant)
const enum LogLevel {
  Info,
  Warning,
  Error,
}

// Alternative to enum (often preferred): union of string literals
// Many teams prefer this over enum because it is simpler and tree-shakeable
type RoleType = "ADMIN" | "EDITOR" | "VIEWER";
```

> **Interview Tip:** A lot of modern TypeScript codebases (including the official TypeScript team's own recommendation) prefer **union of string literals** over `enum` because they are simpler, do not generate extra JavaScript code, and work better with tree-shaking. Still, know `enum` syntax since many companies use it.

---

## Type Assertions

Type assertions tell TypeScript "trust me, I know the type better than you do." Use this carefully — it does not actually convert the value, it just tells the compiler to treat it as a different type.

```typescript
// "as" syntax (preferred, works everywhere including .tsx files)
let value: unknown = "Hello World";
let strLength: number = (value as string).length;

// Angle bracket syntax (does NOT work in .tsx files, avoid in React projects)
let strLength2: number = (<string>value).length;

// Common use case: DOM elements
const input = document.getElementById("email") as HTMLInputElement;
input.value = "test@example.com";  // TypeScript now knows it has a .value property

// Without assertion, TypeScript only knows it is HTMLElement | null
const inputUnsafe = document.getElementById("email");
// inputUnsafe.value = "test"; // Error: Object is possibly 'null', and HTMLElement has no 'value'

// Non-null assertion (!) — tells TypeScript "this is definitely not null/undefined"
function getUser(id: string) {
  const user = users.find(u => u.id === id);
  return user!.name;  // we are SURE user exists, skip the null check
}
// Use this carefully — if you are wrong, you get a runtime error

// "as const" — makes a value deeply readonly and uses literal types instead of general ones
let colors = ["red", "green", "blue"] as const;
// type is now readonly ["red", "green", "blue"] instead of string[]

const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000,
} as const;
// All properties become readonly, and types become literal ("https://..." instead of string)
```

> **Interview Tip:** Type assertions do not perform any real runtime conversion or validation. If you assert something incorrectly, TypeScript will not catch the bug, and you may get an error at runtime instead. Only use assertions when you are absolutely certain about the type.

---

## Any, Unknown, Never, Void

```typescript
// any — disables type checking completely (avoid using this!)
let data: any = 5;
data = "hello";     // no error
data = true;        // no error
data.foo.bar.baz;   // no error, even though this will crash at runtime!

// unknown — like any, but SAFE. You must check the type before using it.
let value: unknown = "Hello";
// value.toUpperCase(); // Error: Object is of type 'unknown'

if (typeof value === "string") {
  value.toUpperCase(); // OK now, TypeScript knows it is a string here
}

// Real difference: any bypasses safety, unknown forces you to check first
function processAny(data: any) {
  return data.toUpperCase();  // compiles fine, may crash at runtime
}

function processUnknown(data: unknown) {
  if (typeof data === "string") {
    return data.toUpperCase();  // safe, TypeScript verified it
  }
  throw new Error("Expected a string");
}

// never — represents values that NEVER occur
// Used for functions that always throw or never finish
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {}
}

// never is also useful for exhaustiveness checking
type Shape = "circle" | "square" | "triangle";

function getArea(shape: Shape): number {
  switch (shape) {
    case "circle":   return 3.14;
    case "square":   return 4;
    case "triangle": return 3;
    default:
      const exhaustiveCheck: never = shape;  // errors if a case is missing!
      return exhaustiveCheck;
  }
}

// void — represents the absence of a return value (used for functions)
function logMessage(message: string): void {
  console.log(message);
  // no return statement, or "return;" with nothing after it
}
```

| Type | Meaning | Safe? |
|---|---|---|
| `any` | Could be anything, all checks disabled | Unsafe — avoid |
| `unknown` | Could be anything, must check before using | Safe |
| `never` | Will never have a value (throws or infinite loop) | N/A |
| `void` | Function returns nothing | N/A |

---

## Optional and Readonly Properties

```typescript
interface UserProfile {
  id: string;
  name: string;
  bio?: string;            // optional: may be undefined
  readonly createdAt: Date; // readonly: can be set once, never changed
}

const profile: UserProfile = {
  id: "1",
  name: "Haseeb",
  createdAt: new Date(),
  // bio is optional, can be left out
};

// profile.createdAt = new Date(); // Error: Cannot assign to 'createdAt' because it is read-only

// Optional chaining works great with optional properties
console.log(profile.bio?.toUpperCase()); // safe, returns undefined if bio is missing

// Optional in function parameters
function updateProfile(id: string, updates?: Partial<UserProfile>) {
  // updates might be undefined, handle accordingly
}

// Optional method
interface EventHandler {
  onClick?: () => void;
  onHover?: () => void;
}
```

---

## Generics

Generics let you write **reusable code that works with multiple types** while still keeping full type safety. Think of generics like a variable, but for types instead of values.

```typescript
// Without generics — you would need a separate function for each type
function getFirstString(arr: string[]): string {
  return arr[0];
}
function getFirstNumber(arr: number[]): number {
  return arr[0];
}
// This gets repetitive fast!

// With generics — ONE function works for ANY type
function getFirst<T>(arr: T[]): T {
  return arr[0];
}

getFirst([1, 2, 3]);          // T is inferred as number, returns number
getFirst(["a", "b", "c"]);    // T is inferred as string, returns string
getFirst<boolean>([true]);    // explicitly specify T

// Generic interfaces
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

interface User {
  id: string;
  name: string;
}

const userResponse: ApiResponse<User> = {
  data: { id: "1", name: "Haseeb" },
  status: 200,
  message: "Success",
};

const usersResponse: ApiResponse<User[]> = {
  data: [{ id: "1", name: "Haseeb" }],
  status: 200,
  message: "Success",
};

// Generic with multiple type parameters
function combine<A, B>(a: A, b: B): [A, B] {
  return [a, b];
}
combine("Haseeb", 23); // type: [string, number]

// Generic constraints (limit what types are allowed)
interface HasLength {
  length: number;
}

function logLength<T extends HasLength>(item: T): void {
  console.log(item.length);
}
logLength("Hello");        // OK, strings have length
logLength([1, 2, 3]);      // OK, arrays have length
// logLength(42);          // Error: number does not have a length property

// Generic classes
class Box<T> {
  private content: T;

  constructor(value: T) {
    this.content = value;
  }

  getValue(): T {
    return this.content;
  }

  setValue(value: T): void {
    this.content = value;
  }
}

const stringBox = new Box<string>("Hello");
const numberBox = new Box<number>(42);

// Default generic type
interface FetchResult<T = unknown> {
  data: T;
  loading: boolean;
}

// Real-world generic example: a reusable fetch hook
function useFetch<T>(url: string): { data: T | null; loading: boolean } {
  // implementation
  return { data: null, loading: true };
}

const { data: user } = useFetch<User>("/api/user");  // data is typed as User | null
```

---

## Classes in TypeScript

```typescript
class Animal {
  // Property declarations with types
  name: string;
  protected age: number;       // accessible in this class and subclasses
  private secretCode: string;  // only accessible inside this class
  readonly species: string;    // can only be set once (in constructor)

  constructor(name: string, age: number, species: string) {
    this.name = name;
    this.age = age;
    this.species = species;
    this.secretCode = "xyz123";
  }

  speak(): string {
    return `${this.name} makes a sound.`;
  }

  protected getAge(): number {
    return this.age;
  }
}

// Shorthand constructor syntax (very common in real codebases)
class Animal {
  constructor(
    public name: string,
    protected age: number,
    private secretCode: string,
    readonly species: string
  ) {}
  // No need to manually assign this.name = name etc. — TypeScript does it for you!

  speak(): string {
    return `${this.name} makes a sound.`;
  }
}

// Inheritance
class Dog extends Animal {
  breed: string;

  constructor(name: string, age: number, breed: string) {
    super(name, age, "default-code", "Dog");
    this.breed = breed;
  }

  speak(): string {
    return `${this.name} barks!`;  // override
  }

  getInfo(): string {
    return `${this.name} is ${this.getAge()} years old.`;  // can access protected method
  }
}

// Abstract classes (cannot be instantiated directly, only extended)
abstract class Shape {
  abstract getArea(): number;   // must be implemented by subclasses

  describe(): string {
    return `This shape has an area of ${this.getArea()}`;
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  getArea(): number {
    return Math.PI * this.radius ** 2;
  }
}

// const shape = new Shape(); // Error: cannot instantiate an abstract class
const circle = new Circle(5);

// Implementing interfaces
interface Flyable {
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

class Duck implements Flyable, Swimmable {
  fly(): void {
    console.log("Flying!");
  }
  swim(): void {
    console.log("Swimming!");
  }
}

// Static properties and methods
class Counter {
  static count: number = 0;

  static increment(): void {
    Counter.count++;
  }
}
Counter.increment();
console.log(Counter.count); // 1

// Getters and setters
class Temperature {
  private _celsius: number = 0;

  get celsius(): number {
    return this._celsius;
  }

  set celsius(value: number) {
    if (value < -273.15) throw new Error("Below absolute zero!");
    this._celsius = value;
  }

  get fahrenheit(): number {
    return (this._celsius * 9) / 5 + 32;
  }
}

const temp = new Temperature();
temp.celsius = 25;
console.log(temp.fahrenheit); // 77
```

---

## Type Narrowing

Narrowing is how TypeScript figures out a more specific type within a block of code based on checks you do.

```typescript
// typeof narrowing
function printValue(value: string | number) {
  if (typeof value === "string") {
    console.log(value.toUpperCase());  // TypeScript knows it is string here
  } else {
    console.log(value.toFixed(2));     // TypeScript knows it is number here
  }
}

// truthy/falsy narrowing
function printName(name: string | null) {
  if (name) {
    console.log(name.toUpperCase());  // TypeScript knows name is not null here
  }
}

// instanceof narrowing
class Cat {
  meow() { console.log("Meow!"); }
}
class Dog {
  bark() { console.log("Woof!"); }
}

function makeSound(animal: Cat | Dog) {
  if (animal instanceof Cat) {
    animal.meow();  // TypeScript knows it is Cat
  } else {
    animal.bark();  // TypeScript knows it is Dog
  }
}

// "in" operator narrowing (check if a property exists)
interface Bird {
  fly(): void;
}
interface Fish {
  swim(): void;
}

function move(animal: Bird | Fish) {
  if ("fly" in animal) {
    animal.fly();   // narrowed to Bird
  } else {
    animal.swim();  // narrowed to Fish
  }
}

// Discriminated unions (the BEST pattern for narrowing complex types)
interface SuccessResult {
  status: "success";
  data: string;
}
interface ErrorResult {
  status: "error";
  message: string;
}
type Result = SuccessResult | ErrorResult;

function handleResult(result: Result) {
  if (result.status === "success") {
    console.log(result.data);     // TypeScript knows this is SuccessResult
  } else {
    console.log(result.message);  // TypeScript knows this is ErrorResult
  }
}

// Custom type guards (functions that tell TypeScript about a type)
interface Cat2 { meow(): void; }
interface Dog2 { bark(): void; }

function isCat(animal: Cat2 | Dog2): animal is Cat2 {
  return (animal as Cat2).meow !== undefined;
}

function handleAnimal(animal: Cat2 | Dog2) {
  if (isCat(animal)) {
    animal.meow();  // TypeScript trusts the type guard
  } else {
    animal.bark();
  }
}
```

---

## Utility Types

TypeScript comes with built-in utility types that transform existing types. These are extremely common in real codebases and interviews.

```typescript
interface User {
  id: string;
  name: string;
  email: string;
  age: number;
}

// Partial<T> — makes all properties optional
type PartialUser = Partial<User>;
// { id?: string; name?: string; email?: string; age?: number }

function updateUser(id: string, updates: Partial<User>) {
  // updates can have any subset of User's properties
}
updateUser("1", { name: "New Name" });  // valid, do not need all fields

// Required<T> — makes all properties required (opposite of Partial)
type RequiredUser = Required<User>;

// Readonly<T> — makes all properties readonly
type ReadonlyUser = Readonly<User>;
const user: ReadonlyUser = { id: "1", name: "Haseeb", email: "h@test.com", age: 23 };
// user.name = "New"; // Error: readonly

// Pick<T, K> — select only specific properties
type UserPreview = Pick<User, "id" | "name">;
// { id: string; name: string }

// Omit<T, K> — exclude specific properties
type UserWithoutEmail = Omit<User, "email">;
// { id: string; name: string; age: number }

// Record<K, T> — create an object type with specific key and value types
type UserRoles = Record<string, "admin" | "user">;
const roles: UserRoles = {
  haseeb: "admin",
  ahmed: "user",
};

type PageVisits = Record<"home" | "about" | "contact", number>;
const visits: PageVisits = { home: 100, about: 50, contact: 25 };

// Exclude<T, U> — remove types from a union
type Status = "active" | "inactive" | "pending" | "deleted";
type ActiveStatus = Exclude<Status, "deleted">;
// "active" | "inactive" | "pending"

// Extract<T, U> — keep only matching types from a union
type StringOrNumber = string | number | boolean;
type OnlyStringOrNumber = Extract<StringOrNumber, string | number>;
// string | number

// NonNullable<T> — remove null and undefined from a type
type MaybeString = string | null | undefined;
type DefinitelyString = NonNullable<MaybeString>;
// string

// ReturnType<T> — get the return type of a function
function createUser() {
  return { id: "1", name: "Haseeb" };
}
type NewUser = ReturnType<typeof createUser>;
// { id: string; name: string }

// Parameters<T> — get the parameter types of a function as a tuple
function greet(name: string, age: number) { }
type GreetParams = Parameters<typeof greet>;
// [name: string, age: number]

// Awaited<T> — unwrap the type inside a Promise
async function fetchUser(): Promise<User> {
  return {} as User;
}
type FetchedUser = Awaited<ReturnType<typeof fetchUser>>;
// User
```

### Quick Reference Table

| Utility | What it does |
|---|---|
| `Partial<T>` | Makes all properties optional |
| `Required<T>` | Makes all properties required |
| `Readonly<T>` | Makes all properties readonly |
| `Pick<T, K>` | Selects specific properties |
| `Omit<T, K>` | Excludes specific properties |
| `Record<K, T>` | Builds an object type from key and value types |
| `Exclude<T, U>` | Removes types from a union |
| `Extract<T, U>` | Keeps only matching types |
| `NonNullable<T>` | Removes null and undefined |
| `ReturnType<T>` | Gets a function's return type |
| `Parameters<T>` | Gets a function's parameter types |

---

## Mapped Types

Mapped types let you create new types by transforming the properties of an existing type. This is actually how utility types like `Partial` and `Readonly` are built internally.

```typescript
// Basic mapped type syntax
type OptionalUser = {
  [K in keyof User]?: User[K];   // this is literally how Partial<T> works
};

// Custom mapped type: make everything nullable
type Nullable<T> = {
  [K in keyof T]: T[K] | null;
};
type NullableUser = Nullable<User>;
// { id: string | null; name: string | null; ... }

// Mapped type with modifiers (+ and - to add/remove readonly or optional)
type Mutable<T> = {
  -readonly [K in keyof T]: T[K];   // removes readonly
};

type AllRequired<T> = {
  [K in keyof T]-?: T[K];   // removes optional (-?)
};

// Mapped type with key remapping (using "as")
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type UserGetters = Getters<User>;
// { getId: () => string; getName: () => string; getEmail: () => string; getAge: () => number }
```

---

## Conditional Types

Conditional types let you choose a type based on a condition, similar to a ternary operator but for types.

```typescript
// Basic syntax: T extends U ? X : Y
type IsString<T> = T extends string ? true : false;

type A = IsString<"hello">;  // true
type B = IsString<42>;        // false

// Practical example
type ApiResponse<T> = T extends string
  ? { message: T }
  : { data: T };

type Response1 = ApiResponse<"Success">;     // { message: "Success" }
type Response2 = ApiResponse<{ id: string }>; // { data: { id: string } }

// infer keyword — extract a type from within another type
type ElementType<T> = T extends (infer U)[] ? U : T;

type Item = ElementType<string[]>;  // string
type Single = ElementType<number>;  // number (not an array, returns as-is)

// Built-in utility types use conditional types internally
// This is roughly how ReturnType<T> works:
type MyReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

// Distributed conditional types (applies to each member of a union)
type ToArray<T> = T extends any ? T[] : never;
type Result = ToArray<string | number>;
// string[] | number[]
```

> **Interview Tip:** Conditional types and mapped types are advanced topics. Most interviews will not deep-dive into writing your own, but you should understand that utility types like `Partial`, `ReturnType`, and `Pick` are built using these mechanisms under the hood.

---

## keyof and typeof Operators

```typescript
// keyof — gets a union of all the property names (keys) of a type
interface User {
  id: string;
  name: string;
  age: number;
}

type UserKeys = keyof User;  // "id" | "name" | "age"

// Practical use: a type-safe property getter
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user: User = { id: "1", name: "Haseeb", age: 23 };
const name = getProperty(user, "name");  // string
const age  = getProperty(user, "age");   // number
// getProperty(user, "email");  // Error: "email" is not a key of User

// typeof — gets the TYPE of a value (used in type positions, not value positions)
const point = { x: 10, y: 20 };
type Point = typeof point;
// { x: number; y: number }

// Combining keyof and typeof — very common real-world pattern
const colors = {
  primary: "#667eea",
  secondary: "#764ba2",
  danger: "#ff4444",
};

type ColorName = keyof typeof colors;
// "primary" | "secondary" | "danger"

function getColor(name: ColorName): string {
  return colors[name];
}
getColor("primary");  // valid
// getColor("warning"); // Error
```

---

## Index Signatures

Index signatures let you describe object types where you do not know the exact property names ahead of time, only their general shape.

```typescript
// Index signature: any string key maps to a number value
interface ScoreBoard {
  [playerName: string]: number;
}

const scores: ScoreBoard = {
  Haseeb: 95,
  Ahmed: 88,
  Sara: 92,
};

scores.Ali = 78;  // valid, any string key is allowed

// Index signature combined with known properties
interface Config {
  apiUrl: string;          // known, required property
  [key: string]: string;   // any other string keys also allowed (must match value type)
}

const config: Config = {
  apiUrl: "https://api.example.com",
  timeout: "5000",  // also allowed because it matches [key: string]: string
};

// Record<K, T> is often a cleaner alternative to index signatures
type ScoreBoard2 = Record<string, number>;
```

---

## Modules and Namespaces

```typescript
// Named exports
// math.ts
export const PI = 3.14159;
export function add(a: number, b: number): number {
  return a + b;
}
export interface Point {
  x: number;
  y: number;
}

// Importing named exports
// main.ts
import { PI, add, Point } from "./math";

// Default export
// user.ts
export default class User {
  constructor(public name: string) {}
}

// Importing default export
import User from "./user";

// Re-exporting
export { add } from "./math";
export * from "./math";
export type { Point } from "./math";  // type-only export

// Type-only imports (useful for clarity, and required in some strict configs)
import type { User } from "./types";
import { type User, someFunction } from "./types";  // mixed import

// Namespaces (older pattern, mostly replaced by ES modules in modern code)
namespace Validation {
  export interface StringValidator {
    isValid(s: string): boolean;
  }

  export class EmailValidator implements StringValidator {
    isValid(s: string): boolean {
      return /\S+@\S+\.\S+/.test(s);
    }
  }
}

const validator = new Validation.EmailValidator();
```

---

## Declaration Files (.d.ts)

Declaration files describe the types for JavaScript code, often for libraries that were not written in TypeScript.

```typescript
// types/global.d.ts — adding types to a JavaScript library

declare module "some-untyped-library" {
  export function doSomething(value: string): boolean;
  export default function init(config: object): void;
}

// Extending an existing global type
declare global {
  interface Window {
    analytics: {
      track: (event: string, properties?: object) => void;
    };
  }
}

// Now anywhere in your app
window.analytics.track("button_clicked", { buttonId: "submit" });

// Declaring types for environment variables
declare namespace NodeJS {
  interface ProcessEnv {
    DATABASE_URL: string;
    API_KEY: string;
    NODE_ENV: "development" | "production" | "test";
  }
}

// Now process.env.DATABASE_URL is typed as string instead of string | undefined
```

---

## TypeScript with React

```tsx
import { useState, useEffect, ReactNode, FC } from "react";

// Typing component props
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: "primary" | "secondary";
  disabled?: boolean;
}

function Button({ label, onClick, variant = "primary", disabled = false }: ButtonProps) {
  return (
    <button className={`btn btn-${variant}`} onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
}

// Typing children
interface CardProps {
  title: string;
  children: ReactNode;
}

function Card({ title, children }: CardProps) {
  return (
    <div className="card">
      <h2>{title}</h2>
      {children}
    </div>
  );
}

// Typing useState
const [count, setCount] = useState<number>(0);
const [user, setUser] = useState<User | null>(null);  // explicit when initial value is null
const [items, setItems] = useState<string[]>([]);

// Typing event handlers
function Form() {
  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
  };

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    console.log(e.target.value);
  };

  const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
    console.log("clicked");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={handleChange} />
      <button onClick={handleClick}>Submit</button>
    </form>
  );
}

// Typing useRef
function FocusInput() {
  const inputRef = useRef<HTMLInputElement>(null);

  const focus = () => {
    inputRef.current?.focus();  // optional chaining since it could be null
  };

  return <input ref={inputRef} />;
}

// Typing custom hooks
function useFetch<T>(url: string): { data: T | null; loading: boolean; error: string | null } {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then((json: T) => setData(json))
      .catch(err => setError(err.message))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}

interface User {
  id: string;
  name: string;
}

function UserProfile({ id }: { id: string }) {
  const { data: user, loading } = useFetch<User>(`/api/users/${id}`);

  if (loading) return <p>Loading...</p>;
  return <h1>{user?.name}</h1>;
}

// Typing context
interface AuthContextType {
  user: User | null;
  login: (email: string, password: string) => Promise<void>;
  logout: () => void;
}

const AuthContext = createContext<AuthContextType | null>(null);

function useAuth(): AuthContextType {
  const context = useContext(AuthContext);
  if (!context) throw new Error("useAuth must be used within AuthProvider");
  return context;
}
```

---

## tsconfig.json Explained

The `tsconfig.json` file controls how TypeScript compiles your project.

```jsonc
{
  "compilerOptions": {
    // Which JS version to compile down to
    "target": "ES2020",

    // Which module system to use
    "module": "ESNext",

    // Catch the most common bugs (always keep this on!)
    "strict": true,

    // Individual strict checks (all included in "strict": true)
    "noImplicitAny": true,         // error if a type cannot be inferred and is implicitly "any"
    "strictNullChecks": true,      // null and undefined are NOT assignable to other types
    "strictFunctionTypes": true,
    "noImplicitThis": true,

    // Module resolution
    "moduleResolution": "bundler",
    "esModuleInterop": true,       // allows default imports from CommonJS modules
    "resolveJsonModule": true,     // allows importing .json files

    // Output
    "outDir": "./dist",
    "declaration": true,           // generate .d.ts files

    // Helpful checks
    "noUnusedLocals": true,        // error on unused variables
    "noUnusedParameters": true,    // error on unused function parameters
    "noFallthroughCasesInSwitch": true,

    // Allow JS files in a TS project (useful during migration)
    "allowJs": true,
    "checkJs": false,

    // JSX support (for React)
    "jsx": "react-jsx",

    // Path aliases
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    },

    // Library types to include
    "lib": ["ES2020", "DOM", "DOM.Iterable"],

    "skipLibCheck": true   // skip type checking of .d.ts files (faster builds)
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

> **Interview Tip:** Always know what `"strict": true` does. It is considered best practice to always enable it on new projects because it catches the most bugs, including the very common "Object is possibly null/undefined" errors.

---

## Common Errors and How to Fix Them

```typescript
// Error: Object is possibly 'undefined'
function getLength(str?: string) {
  return str.length;  // Error!
}
// Fix: check first, or use optional chaining
function getLength(str?: string) {
  return str?.length ?? 0;
}

// Error: Property does not exist on type
const obj = { name: "Haseeb" };
console.log(obj.age);  // Error: Property 'age' does not exist
// Fix: add the property to the type, or use a properly typed object from the start
interface Obj { name: string; age?: number; }

// Error: Type 'X' is not assignable to type 'Y'
let count: number = "5";  // Error
// Fix: use the correct type, or convert it
let count: number = Number("5");

// Error: Argument of type 'X' is not assignable to parameter of type 'Y'
function greet(name: string) { }
greet(42);  // Error
// Fix: pass the correct type
greet("Haseeb");

// Error: Cannot find module or its corresponding type declarations
import _ from "lodash";  // Error if @types/lodash is missing
// Fix: npm install --save-dev @types/lodash

// Error: Element implicitly has an 'any' type because expression of type 'string'
// can't be used to index type '{}'
const colors = { red: "#ff0000", blue: "#0000ff" };
const colorName = "red";
console.log(colors[colorName]);  // Error
// Fix: use keyof typeof, or Record type
function getColor(name: keyof typeof colors) {
  return colors[name];
}

// Error: This condition will always return true/false
let value: string = "hello";
if (value === 42) { }  // Error: types have no overlap
```

---

## Best Practices

```typescript
// 1. Always enable "strict": true in tsconfig.json

// 2. Avoid "any" — use "unknown" when you genuinely do not know the type
function process(data: unknown) {
  if (typeof data === "string") {
    // safely narrowed
  }
}

// 3. Prefer type inference for simple variables, be explicit for function signatures
const age = 23;                                    // let TS infer
function calculateTotal(price: number): number { }  // be explicit

// 4. Use interfaces for object shapes, types for unions/intersections
interface User { name: string; }
type Status = "active" | "inactive";

// 5. Use utility types instead of rewriting similar types
type CreateUserInput = Omit<User, "id" | "createdAt">;

// 6. Use discriminated unions for state that has multiple distinct shapes
type RequestState =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: string }
  | { status: "error"; error: string };

// 7. Avoid type assertions ("as") unless absolutely necessary
// Prefer proper type guards instead

// 8. Use "readonly" for data that should not be mutated
interface Config {
  readonly apiUrl: string;
}

// 9. Name your generic types clearly when there are many
function merge<TFirst, TSecond>(a: TFirst, b: TSecond) { }

// 10. Use path aliases to avoid messy relative imports
// "@/components/Button" instead of "../../../components/Button"
```

---

## Common Interview Questions

### Q1. What is TypeScript and how is it different from JavaScript?
TypeScript is a superset of JavaScript that adds static typing. Every valid JavaScript file is also valid TypeScript. The main difference is that TypeScript checks your code for type errors while you write it (at compile time), while JavaScript only finds errors when the code actually runs. TypeScript is compiled down to plain JavaScript before running in the browser or Node.js.

### Q2. What is the difference between `interface` and `type`?
Both can describe the shape of an object. Interfaces support declaration merging (defining the same interface twice merges them automatically) and use `extends` for inheritance. Type aliases can represent unions, primitives, and tuples directly, and use `&` (intersection) for combining types. A common rule of thumb is to use interfaces for object shapes that might need extending, and types for unions or more complex compositions.

### Q3. What is the difference between `any` and `unknown`?
`any` completely disables type checking — you can do anything with a value typed as `any`, including calling methods that do not exist, without TypeScript complaining. `unknown` is the type-safe version — you must narrow the type (using `typeof`, `instanceof`, or a type guard) before you can do anything with it. Always prefer `unknown` over `any` when you do not know the exact type ahead of time.

### Q4. What are generics and why are they useful?
Generics let you write reusable functions, classes, and interfaces that work with multiple types while keeping full type safety. Instead of writing a separate function for each type, or using `any` and losing type safety, you use a placeholder type like `T` that gets filled in when the function is actually called. A classic example is `Array<T>` itself, or a `useFetch<T>` hook that can fetch any type of data.

### Q5. What is type narrowing?
Type narrowing is how TypeScript figures out a more specific type from a broader one, based on checks you write in your code. For example, checking `typeof value === "string"` narrows a `string | number` type down to just `string` within that block. Common narrowing techniques include `typeof`, `instanceof`, the `in` operator, truthy checks, and discriminated unions.

### Q6. What are utility types? Name a few and explain what they do.
Utility types are built-in generic types that transform other types. `Partial<T>` makes all properties optional. `Required<T>` makes them all required. `Pick<T, K>` selects specific properties. `Omit<T, K>` excludes specific properties. `Readonly<T>` makes all properties readonly. `Record<K, T>` builds an object type from key and value types. They save you from manually rewriting variations of the same type.

### Q7. What is a discriminated union and why is it useful?
A discriminated union is a pattern where you combine several object types using a common property (often called a "discriminant" or "tag") that has a different literal value in each type, like `status: "success"` vs `status: "error"`. TypeScript can then narrow the type automatically based on a check of that property, which is extremely useful for representing things like API response states cleanly and safely.

### Q8. What does `strict: true` do in tsconfig.json?
It enables a group of strict type-checking options, including `strictNullChecks` (null and undefined are not assignable to other types unless explicitly allowed), `noImplicitAny` (errors when a type cannot be inferred), and several others. It is considered best practice to always enable strict mode on new projects because it catches the most bugs, particularly issues with null and undefined values.

### Q9. What is the difference between `type` assertion and type casting (like in other languages)?
TypeScript's `as` syntax (type assertion) does not perform any actual runtime conversion — it simply tells the TypeScript compiler "trust me, treat this value as this type" without checking if that is actually true. This is different from real type casting in languages like Java or C#, where the runtime actually verifies and converts the value. If you assert incorrectly in TypeScript, you will not get a compile error, but you might get a runtime crash.

### Q10. How do generics with constraints work?
You can limit what types are allowed for a generic using `extends`. For example, `function logLength<T extends { length: number }>(item: T)` only accepts types that have a `length` property, like strings or arrays. This gives you the flexibility of generics while still ensuring the type has the properties or methods your function actually needs.

### Q11. What is the purpose of the `keyof` operator?
`keyof` takes an object type and produces a union of its property names as string literal types. For example, `keyof User` for a `User` interface with `name` and `age` properties gives you `"name" | "age"`. This is extremely useful for writing type-safe functions that access object properties dynamically, like a generic `getProperty(obj, key)` function.

### Q12. What happens to TypeScript types at runtime?
Nothing — TypeScript types are completely erased during compilation. They only exist to help you and your editor catch mistakes while writing code. The final JavaScript output has no trace of types, interfaces, or generics. This is why you cannot, for example, check `typeof someValue === "User"` at runtime — types are a compile-time-only concept.

### Q13. What is the difference between `null` and `undefined` in TypeScript, and what is `strictNullChecks`?
`undefined` usually means a variable has been declared but not assigned. `null` is an explicit "no value" assignment. By default (without `strictNullChecks`), TypeScript allows you to assign `null` or `undefined` to any type, which can hide bugs. With `strictNullChecks` enabled (part of `strict: true`), you must explicitly include `| null` or `| undefined` in a type if you want to allow those values, forcing you to handle the missing-value case properly.

### Q14. What is declaration merging?
Declaration merging is a TypeScript feature, unique to interfaces, where defining the same interface name multiple times automatically combines all the properties into one. This is commonly used to extend global types, like adding a custom property to the `Window` interface, or to allow a library's consumers to extend its types without modifying the library's source code.

### Q15. How do you type a React component's props in TypeScript?
You define an interface or type describing the expected props, then use it as the type for the function's parameter. For example, `interface ButtonProps { label: string; onClick: () => void; }` followed by `function Button({ label, onClick }: ButtonProps) { }`. For children, use the `ReactNode` type from React. For event handlers, use React's built-in event types like `React.ChangeEvent<HTMLInputElement>` or `React.FormEvent<HTMLFormElement>`.

---

## Contributing

Found a mistake or want to add something? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Next.js, TypeScript, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).