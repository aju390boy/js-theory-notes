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
### nullable type
Sometimes a value may be absent initially, so we allow null as one of its possible types. Later, when the actual data becomes available, the variable can hold that data instead of null. We usually represent this using a union type.
```ts
let user: User | null = null;
//initially : user → null
user = {
    name: "Ajith",
    age: 22
};
// Later: user → User object
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
### Intersection Type
An intersection type combines two or more types into a single type using the & operator. The resulting value must satisfy all the combined types.
```ts
type A = {
    name: string;
};

type B = {
    age: number;
};

type Person = A & B;
```
Now Person must contain both name and age.
```ts
const user: Person = {
    name: "Ajith",
    age: 22
};
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

### Type Assertion
Type assertion is a TypeScript feature used during the compilation phase to tell the TypeScript compiler to treat a value as a specific type when the developer knows more about that value's type than the compiler does. It does not change the actual value or its runtime type.
Example 1:
```ts
let value: unknown;
value = "ajith"; // compile phase:value is string ,but its type still unknown
console.log(value.charAt(0)); // ERROR
```
Example 2:
```ts
let value: unknown; 
value = "ajith"; // compile phase:value is string ,but its type still unknown

let name = value as string; // compile phase:name's value is string and its type also string.

console.log(name.charAt(0)); // SUCCESS
```
* In both cases, the runtime type will be string. ✅
TypeScript is statically typed, so during the compilation phase the tsc compiler checks a variable based on its static type. Even if an unknown variable currently contains a string at runtime, TypeScript still treats it as unknown unless the type is narrowed or asserted. Therefore, string methods cannot be used directly. A type assertion such as value as string tells the compiler to treat that expression as a string, allowing string operations. The assertion does not change the actual runtime value or perform any conversion.


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

## Type Alias
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



# OOPs

## Phase 1: The Mindset Shift – Nominal vs. Structural Typing

[![DUCK TYPING](https://img.shields.io/badge/JavaScript-yellow)](https://img.shields.io/badge/JavaScript-yellow)
                          
In Java, the class name is the most important thing. Even if two classes have the exact same variables inside, Java treats them as 100% different because Java is a nominal typed language (names matter).

In TypeScript, the type of an object is determined by its shape (its properties and methods) rather than its name. This is called structural typing, or Duck Typing. If a plain object or a different class has the exact properties required by a type, TypeScript considers it a perfect match—even if they have different names or you never used the new keyword.

### Example 1: Class A and Class B are Interchangeable
Because TypeScript only checks the shape, two completely different classes can be mixed if their internal structure is exactly the same.
```ts
// Class A
class CashPayment {
  amount: number;
  currency: string;
}

// Class B
class CardPayment {
  amount: number;
  currency: string;
}

// In Java: ERROR! "A CardPayment is not a CashPayment!"
// In TypeScript: SUCCESS! Both have 'amount' and 'currency'.
let myPayment: CashPayment = new CardPayment();
```
### Example 2: Plain Objects without the new keyword
When you fetch data from a database or API, it comes as a plain object. Duck typing allows you to safely check that plain data against a Class type without ever needing to build a real class object using new.
```ts
class Product {
  name: string;
  price: number;
}

// Just a plain JavaScript object (like data from an API)
let dbData = {
  name: "Riding Helmet",
  price: 8799
};

// SUCCESS! TypeScript sees the plain object has 'name' and 'price'.
// It perfectly fits the shape of the Product class.
let myItem: Product = dbData;
```
### Example 3: Error Prevention (The Shape Must Match)
Duck typing is a strict rule to prevent runtime crashes. If the object you are passing is missing even one required piece of the shape, TypeScript will instantly block it.
```ts
class User {
  name: string;
  email: string;
}

// ERROR! 
// TypeScript says: "Property 'email' is missing." 
// The shape is broken, so it is not a valid User.
let badUser: User = { 
  name: "Ajith" 
};
```

### BYPASSING INHERITANCE (Bypassing inheritance is the superpower you get because of Duck typing rule)
In java,To make a function accept either Class A or Class B, Java forces you to create an interface and use the implements keyword.
```java
// The Interface creates the shared "name" for nominal typing
interface Order {
    void process(); 
}

class Online implements Order {
    public void process() { System.out.println("online..."); }
}

class Offline implements Order {
    public void process() { System.out.println("offline..."); }
}

public class Main {
    // Now you only need one method!
    public static void processOrder(Order myOrder) {
        myOrder.process(); 
    }
}
```
Thanks to Duck Typing, you bypass inheritance entirely. No extends or implements needed! If two classes just happen to have the same shape, they work together automatically. Even 3rd-party classes work instantly without touching their code, as long as the shape matches.
```java
// Class A (100% independent)
class OnlineOrder {
  process() { console.log("Processing online..."); }
}

// Class B (100% independent)
class StoreOrder {
  process() { console.log("Processing in-store..."); }
}

// This function doesn't care about class names or interfaces.
// It just asks: "Does the object have a process() method?"
function handleOrder(order: { process: () => void }) {
  order.process();
}

let webOrder = new OnlineOrder();
let shopOrder = new StoreOrder();

// SUCCESS! 
// Both work perfectly without ever using "extends" or "implements"!
handleOrder(webOrder);
handleOrder(shopOrder);
```
### Compile time vs Runtime
TypeScript types, interfaces, and structural checks only exist at compile-time. At runtime, the JavaScript engine executes the code blindly, with no memory of the TypeScript rules.
 
## GENERICS
## Interface
## Class
## Dependency Injection
## Narrowing
## Mixins
## Decorators
## Duck Typing
## inheritance