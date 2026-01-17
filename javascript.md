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

## Functions & Scope

### Q: What is a Closure?
**A:** A closure is a function that remembers its outer variables and can access them even when the function is executed outside its original scope.

```javascript
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}