# new Keyword
### 1. The Manual Way (No new keyword)
If you do not use new, you must manually build the connection to your methods for every single instance.
```js
// A shared bucket of methods
const methods = {
    print() { console.log(`my name is ${this.name}`); }
};

// You must manually wire everything together
let a = {};
Object.setPrototypeOf(a, methods); // Manual linking
a.name = 'ajith';                  // Manual property assignment

a.print();
```
### 2. The Automated Way (With new)
The new keyword replaces all that manual wiring with a single word.
```js
class A {
    constructor(name) {
        this.name = name; // You only worry about the data
    }
    print() {
        console.log(`my name is ${this.name}`);
    }
}

let a = new A('ajith'); // Automation handles the rest
a.print();
```
### The Core Theory in 3 Rules
* Isolation: It ensures that this.name = 'ajith' only affects the specific variable a, without leaking data or breaking other variables.
* Shared Memory: It ensures that the print() function is stored exactly once in memory, rather than being duplicated for every new user you create.
* The Strict Rule: JavaScript enforces new on classes to prevent you from accidentally running a class like a normal function, which would crash your application or corrupt global data.