# The Doubly Linked List (DLL)

 **The Concept:** In a normal list, you can only walk forward. If you drop something behind you, you have to start all the way from the beginning to find it. In a Doubly Linked List, every node has two pointers: one pointing forward (next) and one pointing backward (prev).


### THE DOUBLY NODE
```js
class DoublyNode {
  constructor(value) {
    this.value = value;
    this.next = null; // Points to the next node
    this.prev = null; // NEW: Points to the previous node
  }
}
```

### THE DOUBLY LINKED LIST
```js
class DoublyLinkedList {
  constructor() {
    this.head = null; // The front
    this.tail = null; // The back
    this.size = 0;
  }

  append(value) {
    const newNode = new DoublyNode(value);

    // Scenario A: The list is empty
    if (this.size === 0) {
      this.head = newNode;
      this.tail = newNode; // The first node is both the head and the tail
    } 
    // Scenario B: The list has items
    else {
      this.tail.next = newNode; // 1. The old tail reaches forward to grab the new node
      newNode.prev = this.tail; // 2. The new node reaches backward to grab the old tail
      this.tail = newNode;      // 3. Move the official "tail" sign to the new node
    }
    this.size++;
  }
  prepend(value) {
    const newNode = new DoublyNode(value);

    // Scenario A: The list is empty
    if (this.size === 0) {
      this.head = newNode;
      this.tail = newNode;
    } 
    // Scenario B: The list has items
    else {
      newNode.next = this.head; // 1. New guy reaches forward to old Head
      this.head.prev = newNode; // 2. Old Head reaches backward to new guy
      this.head = newNode;      // 3. Move the official "Head" sign to the new guy
    }
    this.size++;
  }
  
  removeValue(value) {
    if (this.size === 0) return null; // Empty list

    let current = this.head;

    // Step 1: Walk through the list to find the value
    while (current !== null && current.value !== value) {
      current = current.next;
    }

    // Step 2: Did we find it? If current is null, we reached the end without finding it.
    if (current === null) return null; 

    // Step 3: Deleting the node...
    
    // Scenario A: It's the ONLY node in the list
    if (this.size === 1) {
      this.head = null;
      this.tail = null;
    } 
    // Scenario B: It's the HEAD (first node)
    else if (current === this.head) {
      this.head = this.head.next; // Move head to the second node
      this.head.prev = null;      // Remove the backward hook to the deleted node
    } 
    // Scenario C: It's the TAIL (last node)
    else if (current === this.tail) {
      this.tail = this.tail.prev; // Move tail back one spot
      this.tail.next = null;      // Remove the forward hook to the deleted node
    } 
    // Scenario D: It's in the MIDDLE (The magic happens here)
    else {
      current.prev.next = current.next; // A points to C
      current.next.prev = current.prev; // C points to A
    }

    this.size--;
    return current.value;
  }
  // The cool part: We can print backward easily!
  printReverse() {
    let current = this.tail; // Start at the end
    let output = "";
    
    while (current) {
      output += `${current.value} <-> `;
      current = current.prev; // Walk backwards!
    }
    console.log("null <-> " + output + "null");
  }
}

// Test it:
const dll = new DoublyLinkedList();
dll.append(10);
dll.append(20);
dll.append(30);
dll.printReverse(); // Output: null <-> 30 <-> 20 <-> 10 <-> null
```

### The Magic of Deletion

* In a normal (Singly) Linked List, deleting is a headache. If you find the guy you want to delete, you have to run all the way through the list again just to find the guy before him so you can fix the hook.

* In a Doubly Linked List, the guy you are deleting is already holding the hands of both neighbors! You just tell his neighbors to let go of him and grab each other.

The Logic:
Let's say we have: Node A <-> Node B <-> Node C. We want to delete B.

* Find B.
* Tell A (B.prev) to point forward to C (B.next).
* Tell C (B.next) to point backward to A (B.prev).
* B is now completely disconnected and floats away.