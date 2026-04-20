```js
class Node {
    constructor(value) {
        this.value = value; // The actual data
        this.next = null;   // The pointer to the node directly beneath this one
    }
}

class LinkedListStack {
    constructor() {
        this.top = null; // Starts empty
        this.size = 0;
    }

    // PUSH: Add a new node to the top
    push(value) {
        const newNode = new Node(value);
        
        // 1. The new node points down to whatever used to be the top
        newNode.next = this.top; 
        
        // 2. The new node is officially declared the new top
        this.top = newNode;      
        this.size++;
    }

    // POP: Remove and return the top node
    pop() {
        if (this.isEmpty()) return "Stack Underflow";

        const poppedValue = this.top.value; // Save the value to return later
        
        // Move the 'top' pointer down one level, severing the old top
        this.top = this.top.next; 
        this.size--;
        
        return poppedValue;
    }

    // PEEK: Look at the top value without removing it
    peek() {
        if (this.isEmpty()) return "Stack is empty";
        return this.top.value;
    }

    // Helper to check if it's empty
    isEmpty() {
        return this.top === null;
    }
    
    // Helper to print the stack from top to bottom
    print() {
        let current = this.top;
        let result = [];
        while (current) {
            result.push(current.value);
            current = current.next;
        }
        console.log(result.join(" -> "));
    }
}

const myStack = new LinkedListStack();

myStack.push(10);
myStack.push(20);
myStack.push(30);

myStack.print(); 
// Output: 30 -> 20 -> 10

console.log("Popped:", myStack.pop()); 
// Output: Popped: 30

myStack.print(); 
// Output: 20 -> 10
```