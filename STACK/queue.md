```js
class StackWithOneQueue {
    constructor() {
        this.queue = [];
    }

    // PUSH: Add the item, then rotate the queue
    push(value) {
        // Step 1: Add the new item to the back
        this.queue.push(value);

        // Step 2: Find out how many OLD items are in front of it
        // (We subtract 1 because we don't want to rotate the new item we just added)
        let previousSize = this.queue.length - 1;

        // Step 3: Rotate the queue
        // Take an item from the front and move it to the back
        for (let i = 0; i < previousSize; i++) {
            let oldItem = this.queue.shift(); // Remove from front
            this.queue.push(oldItem);         // Add to back
        }
    }

    // POP: The newest item was rotated to the front, so just dequeue it!
    pop() {
        if (this.isEmpty()) return "Stack is empty";
        return this.queue.shift();
    }

    peek() {
        if (this.isEmpty()) return "Stack is empty";
        return this.queue[0];
    }

    isEmpty() {
        return this.queue.length === 0;
    }
}

// --- Let's test the One Queue version! ---
const myStack = new StackWithOneQueue();

myStack.push(10);
myStack.push(20);
myStack.push(30); 

// Because of our rotation, the queue currently looks like this inside: [30, 20, 10]

console.log(myStack.pop()); // Outputs: 30 (Last in, First out!)
console.log(myStack.pop()); // Outputs: 20
```