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


## Infer OR Type Inference
Type inference means TypeScript automatically guesses the type of a variable based on the value you assign to it. So, you don't always need to write the type yourself.
```ts
let name = "Ajith";
//TypeScript automatically understands:
let name: string = "Ajith";
```
## TSC


## GENERICS