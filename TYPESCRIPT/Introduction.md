# TYPESCRIPT

* In simple words : Javascript with type checking and code complation,refactoring,new features....

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
| Example string | number | `Example: yes  no` |
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

## TSC


## GENERICS