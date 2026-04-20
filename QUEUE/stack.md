```js
class QueueWithTwoStacks {
    constructor() {
        // We only use .push() and .pop() on these arrays to simulate strict Stacks
        this.stack1 = []; // Used for enqueueing
        this.stack2 = []; // Used for dequeueing
    }

    // ENQUEUE: Just add the new item to the top of Stack 1
    // This is incredibly fast (O(1) time)
    enqueue(value) {
        this.stack1.push(value);
    }

    // DEQUEUE: Remove the oldest item
    dequeue() {
        // If both stacks are completely empty, we have an underflow
        if (this.stack1.length === 0 && this.stack2.length === 0) {
            return "Queue is empty";
        }

        // If Stack 2 is empty, we need to pour everything from Stack 1 into it.
        // This process REVERSES the order of the items!
        if (this.stack2.length === 0) {
            while (this.stack1.length > 0) {
                let poppedItem = this.stack1.pop(); // Take from top of Stack 1
                this.stack2.push(poppedItem);       // Put on top of Stack 2
            }
        }

        // Now, the oldest item is sitting right at the top of Stack 2
        return this.stack2.pop();
    }

    // PEEK: Look at the front of the line without removing them
    peek() {
        if (this.stack1.length === 0 && this.stack2.length === 0) {
            return "Queue is empty";
        }

        // Just like dequeue, if stack2 is empty, we must pour stack1 over first
        if (this.stack2.length === 0) {
            while (this.stack1.length > 0) {
                this.stack2.push(this.stack1.pop());
            }
        }

        // Return the top of Stack 2 (which is the last element in the array)
        return this.stack2[this.stack2.length - 1];
    }
}
```