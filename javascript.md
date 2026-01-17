# JavaScript Theory Repository

## Table of Contents
1. [Core Concepts](#core-concepts)
2. [Functions & Scope](#functions--scope)
3. [Asynchronous JS](#asynchronous-js)
4. [DOM Manipulation](#dom-manipulation)

---

## Core Concepts

### Q: What are the data types in JavaScript?
**A:** There are 8 data types:
* **Primitive:** String, Number, BigInt, Boolean, Undefined, Null, Symbol.
* **Reference:** Object.

### Q: Difference between == and ===?
**A:** * `==` checks for value (allows type coercion).
* `===` checks for value AND type (strict equality).

---

### Q: enum?
**A:** Actually,Enum is NOT a data type in JavaScript.
* JavaScript does not have a built-in enum keyword like Java or TypeScript.
* Enum is a predefined set of allowed values used to control what data can be stored in a field.

### Q: Promisify?
* Promisify is a technique used to convert existing callback-based asynchronous functions into promise-based functions.
* promisify is closely related to callbacks and promises. Both callbacks and promises are used to handle asynchronous operations in JavaScript. Callbacks were introduced first, but they caused issues such as callback hell and difficulty in debugging. To overcome these problems, promises were introduced.

### Q: Starvation?
* Starvation in JavaScript is a situation where some tasks never get a chance to execute because other tasks keep getting priority again and again.
* Starvation is a condition where a task is indefinitely postponed because higher-priority tasks continuously consume execution time.

### Q: Just-In-Time (JIT)?
* Modern JavaScript engines use JIT compilation to improve performance by compiling code into machine code at runtime. JavaScript does not require specifying variable data types because it is a dynamically typed language.
