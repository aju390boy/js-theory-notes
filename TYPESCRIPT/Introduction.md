# TYPESCRIPT

* In simple words : Javascript with type checking and code complation,refactoring,new features....

## TSC

## Better IntelliSense (autocomplete)
TypeScript also provides better IntelliSense by suggesting only the valid built-in methods and properties for that type, helping catch errors while coding.

Example
```ts
let name: string = "Ajith";
```
When you type:
```ts
name.
```
VS Code suggests only string methods, such as:
* toUpperCase()
* toLowerCase()
* trim()
* slice()
* includes()

It won't suggest methods that don't belong to strings.
Also same as number,Array,object,etc..

## Unused Variable

* TypeScript compiler catches unused variables to prevent dead code from reaching production.
* TypeScript compiler is strictly enforcing code quality rules.
* TypeScript typically ignores unused variables that start with _.
* variable name is 'a' and unused,gets an error but we can use like '_a'.

## Statically Typed languages
* Typescript
* C#
* JAVA
* C++

## Dynamically Typed languages
* Javascript
* Python
* Ruby

## JavaScript vs TypeScript Data Types
| JavaScript | TypeScript |
|------------|------------|
| Number | `any` |
| String | `unknown` |
| Boolean | `enum` |
| `null` | `never` |
| Object | `tuple` |
| `undefined` |  |

### any
any can store any type of value. TypeScript does not check its type.
```ts
let data: any = "Ajith";
data = 25;
data = true;
```
### unknown
unknown can store any value, but you must check its type before using it.
```ts
let value: unknown = "Hello";

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```
### enum
enum is used to create a group of named constant values.
It improves code readability, type safety, and prevents invalid values by restricting a variable to a predefined set of constants.
Provides auto-completion in editors,And it is commonly used for statuses, roles, and categories.
```ts
enum Status {
  Pending,
  Success,
  Failed
}

let orderStatus: Status = Status.Success;
```
### never
never is used for functions that never return a value, such as functions that always throw an error.
```ts
function showError(message: string): never {
  throw new Error(message);
}
```
### tuple
A tuple stores a fixed number of values with specific types in a specific order.
A tuple is a special type of array in TypeScript where the number of elements and the type of each element are fixed.
A tuple cannot exist without an array because tuples are represented using array syntax ([]).
```ts
let user: [string, number] = ["Ajith", 22];
```
### Union Type (|)
A Union Type allows a variable to store more than one type of value.
```TS
let id: string | number;

id = "EMP101";
id = 101;

// Another example

function printId(id: string | number) {
  console.log(id);
}
```
### Literal Type
A Literal Type allows a variable to store only specific values.
```ts
let direction: "left" | "right";

direction = "left";   // ✅
direction = "right";  // ✅
direction = "up";     // ❌ Error

//Another example

type Status = "pending" | "success" | "failed";

let orderStatus: Status = "success";
```
## Difference Between Union Type and Literal Type
| Union Type | Literal Type |
|------------|------------|
| Allows multiple types | `Allows only specific values` |
| Example : string number(types) | `Example: yes  no(values)` |
| Stores different data types | `Restricts the allowed values` |

```ts
// Union Type
let age: string | number;
age = 22;
age = "Twenty Two";

// Literal Type
let role: "admin" | "user";
role = "admin";   // ✅
role = "guest";   // ❌ Error
```
* Union Type → One variable, multiple types.
* Literal Type → One variable, fixed allowed values.

## Custom Types
TypeScript allows developers to create reusable custom types.

### type
```ts
type User = {
  name: string;
  age: number;
};

let person: User = {
  name: "Ajith",
  age: 22
};
```
### interface
```ts
interface User {
  name: string;
  age: number;
}

let person: User = {
  name: "Ajith",
  age: 22
};
```
## Infer OR Type Inference
Type inference means TypeScript automatically guesses the type of a variable based on the value you assign to it. So, you don't always need to write the type yourself.
```ts
let name = "Ajith";

//TypeScript automatically understands:

let name: string = "Ajith";
```

## Array
An array in TypeScript is the same as a JavaScript array, but all elements must follow the specified type.
The only difference is that TypeScript checks the type of the array elements, helping catch errors during development.
```ts
let numbers: number[] = [10, 20, 30];

//or

let names: Array<string> = ["Ajith", "Arun", "Rahul"];

//or

let data: (string | number)[] = ["Ajith", 22, "MERN"];
```
## Function
A function in TypeScript is the same as a JavaScript function, but with type annotations for parameters and return values. 
This helps catch errors during development and provides better code completion and documentation.
```ts
function add(a: number, b: number): number {
  return a + b;
}

add(10, 20); // 30
```
Here:
* a: number → parameter type
* b: number → parameter type
* : number → return type

## Features of Functions in TypeScript

### 1. Typed Parameters
Specify the type of each parameter.
```ts
function greet(name: string) {
  return `Hello ${name}`;
}
```
### 2. Return Type
Specify what type the function returns.
```ts
function square(num: number): number {
  return num * num;
}
```
### 3. Optional Parameters (?)
```ts
function greet(name: string, age?: number) {
  console.log(name, age);
}

greet("Ajith");
greet("Ajith", 22);
```
### 4. Default Parameters
```ts
function greet(name: string = "Guest") {
  console.log(name);
}

greet();       // Guest
greet("Ajith");
```
### 5. Rest Parameters
```ts
function total(...numbers: number[]): number {
  return numbers.reduce((sum, n) => sum + n, 0);
}

total(10, 20, 30);
```
### 6. Arrow Functions
```ts
const divide = (a: number, b: number): number => {
  return a / b;
};
```
### 7. Void Functions
```ts
function printMessage(msg: string): void {
  console.log(msg);
}
```
### 8. Never Return Type
A function with the never return type never returns a value to its caller.
Because the function either:throws an error, or runs forever (infinite loop).
Since execution never reaches the caller again, TypeScript says the return type is never,"The function never finishes".
```ts
function throwError(message: string): never {
  throw new Error(message);
}
```
### 9. Function Type
A function type is a blueprint or signature of a function that tells TypeScript what kind of function is allowed.
It specifies what parameters the function should accept and what type of value it should return.
This is a function type declaration,It is not the function itself.

This line only declares the variable and its type,The variable doesn't contain a function yet.
```ts
let add: (a: number, b: number) => number;
```
It's like this:
```ts
let age: number;
```
Definitions of that function:
```ts
add = function(a, b) {
    return a + b;
};
```
OR
```ts
add = (a, b) => a + b;
```
Function Type mostly use in Callbacks:
```ts
function calculate(
    operation: (a: number, b: number) => number
) {
    console.log(operation(10, 20));
}
```
Now you can pass
```ts
calculate((a, b) => a + b);

calculate((a, b) => a * b);
```

### 10. Function Overloading
Function overloading is a TypeScript feature that allows one function to have multiple valid signatures,while using only one implementation.
Function overloading tells TypeScript that a function can be called in different ways.
Function overloading is preferred over a union type(|) when the return type depends on the parameter type. While union types(|) allow multiple input types, overloads let TypeScript infer a more specific return type for each valid function signature.

Suppose we write this with a union(|).
```ts
function getUser(value: number | string) {
    if (typeof value === "number") {
        return "One User";
    }

    return ["User1", "User2"];
}
```
Now imagine you call it.
```ts
const result = getUser(1);
```
What is the type of result?
You might think : 
```ts
string
```
But TypeScript says:
```ts
string | string[]
```
Why?
Because the function could return either one.TypeScript only sees the whole function, not the path you're taking.
Even though you know it's actually a string.

Now Let's Use Overloading
```ts
function getUser(id: number): string;
function getUser(email: string): string[];

function getUser(value: number | string) {
    if (typeof value === "number") {
        return "One User";
    }

    return ["User1", "User2"];
}
```
```ts
const result1 = getUser(1);
```
TypeScript knows
```ts
result1 // string ✅
```
and
```ts
const result2 = getUser("admin@gmail.com");
```
TypeScript knows
```ts
result2 // string[] ✅
```
That's the big advantage of overloads.

## Type alias
A type alias is a TypeScript feature that allows us to create a custom name for an existing type or a combination of types. 
It improves code readability, reusability, and maintainability.
* Type alias = giving a reusable name to a type.
```ts
type Age = number;
// then
let myAge: Age = 22;
```
OR
```ts
type User = {
    name: string;
    age: number;
};
```
Here User or Age is just a name for that type, not an actual object or variable.

### Think of it like a shortcut name
```ts
type User = {
    name: string;
    age: number;
};
```
"Whenever I say User, I mean this entire structure."
So:
```ts
let user: User;
```
is basically the same as:
```ts
let user: {
    name: string;
    age: number;
};
```
A type alias does not create a new runtime value such as an object or variable. It gives a name to a type definition, allowing that type to be reused. 
Type aliases are used only by TypeScript's type system and do not exist at runtime.


## OOPs
## GENERICS
## Interface
## Class