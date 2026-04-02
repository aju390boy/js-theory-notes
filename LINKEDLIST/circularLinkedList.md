# The Circular Linked List (CLL)

**The Concept:** A Circular Linked List is usually just a Singly Linked List, but with one major rule change: There is no dead end. Instead of the last node pointing to null, the last node's next pointer loops all the way back around to grab the head.

* The most important rule to remember when reading this code: If the head ever changes, the tail must be updated to point to the new head!

### THE CIRCULAR NODE

```js 
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```
### THE CIRCULAR LINKEDLIST

```js
class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // --- 1. ADD TO END (No Loop Needed) ---
  append(value) {
    const newNode = new Node(value);

    if (this.size === 0) {
      this.head = newNode;
      this.tail = newNode;
      newNode.next = this.head; // Point to itself to make a circle
    } else {
      this.tail.next = newNode;   // 1. Old tail points forward to new guy
      this.tail = newNode;        // 2. Move the "Tail" sign to the new guy
      this.tail.next = this.head; // 3. The new tail points back to the start!
    }
    this.size++;
  }

  // --- 2. ADD TO FRONT (No Loop Needed) ---
  prepend(value) {
    const newNode = new Node(value);

    if (this.size === 0) {
      this.head = newNode;
      this.tail = newNode;
      newNode.next = this.head;
    } else {
      newNode.next = this.head;   // 1. New guy points to the old Head
      this.head = newNode;        // 2. Move the "Head" sign to the new guy
      this.tail.next = this.head; // 3. CRITICAL: Tell the tail where the NEW head is!
    }
    this.size++;
  }

  // --- 3. DELETE A VALUE (Loop Needed to Search) ---
  removeValue(value) {
    if (this.size === 0) return null; // Empty list

    // SCENARIO A: The list only has 1 item, and it's the one we want to delete
    if (this.size === 1 && this.head.value === value) {
      this.head = null;
      this.tail = null;
      this.size = 0;
      return value;
    }

    // SCENARIO B: We are deleting the HEAD (but there are other items)
    if (this.head.value === value) {
      this.head = this.head.next; // Move head to the second item
      this.tail.next = this.head; // CRITICAL: Tell the tail where the NEW head is
      this.size--;
      return value;
    }

    // SCENARIO C: Deleting from the Middle or the Tail
    let current = this.head;
    
    // Look ahead to find the value! 
    // Stop if we circle all the way back to the head.
    while (current.next !== this.head && current.next.value !== value) {
      current = current.next;
    }

    // If we found it...
    if (current.next.value === value) {
      
      // Is the guy we are deleting the TAIL?
      if (current.next === this.tail) {
        this.tail = current;        // Move the "Tail" sign back one spot
        this.tail.next = this.head; // Make sure new tail points to the head
      } 
      // It's just a normal guy in the middle
      else {
        current.next = current.next.next; // Skip over the deleted node
      }
      
      this.size--;
      return value;
    }

    return null; // Value was not found in the circle
  }

  // --- 4. SHOW THE LIST (do...while loop) ---
  print() {
    if (this.size === 0) {
      console.log("List is empty");
      return;
    }

    let current = this.head;
    let output = "";

    // We use a do...while loop so we print the first item BEFORE 
    // checking if we accidentally hit the start again.
    do {
      output += `${current.value} -> `;
      current = current.next;
    } while (current !== this.head); 

    console.log(output + "(Back to Head)");
  }
}

// === LET'S TEST IT! ===
const cll = new CircularLinkedList();

console.log("1. Add items to the end:");
cll.append("A");
cll.append("B");
cll.append("C");
cll.print(); 
// Output: A -> B -> C -> (Back to Head)

console.log("\n2. Add 'Start' to the front:");
cll.prepend("Start");
cll.print(); 
// Output: Start -> A -> B -> C -> (Back to Head)

console.log("\n3. Delete 'B' (Middle):");
cll.removeValue("B");
cll.print(); 
// Output: Start -> A -> C -> (Back to Head)

console.log("\n4. Delete 'C' (Tail):");
cll.removeValue("C");
cll.print(); 
// Output: Start -> A -> (Back to Head)

console.log("\n5. Delete 'Start' (Head):");
cll.removeValue("Start");
cll.print(); 
// Output: A -> (Back to Head)
```
### 1. The Golden Rule
The tail must always point to the head.
If you change who the head is, you must tell the tail. If you change who the tail is, the new tail must point to the head. If you forget this, the circle breaks and it just becomes a normal, broken list.

### 2. The Danger Zone (Infinite Loops)
In a normal list, you use while (current !== null) because you know the road ends.
In a circular list, there is no null. If you write a normal while loop, your code will run forever and crash your browser.

The Fix: Always save the starting point (this.head) and stop the loop when you see that exact node again. (This is why do...while loops are perfect here).

### 3. The "Tail" Cheat Code
Just like in the Doubly Linked List, keeping a this.tail variable is a superpower. Because the tail is directly connected to the head, having the tail means you have instant access to both the very front and the very back of the circle without having to loop through it.

### 4. When to actually use it in the real world
You won't use this every day, but when you need it, nothing else works better.

Multiplayer Games: (Player 1 -> Player 2 -> Player 3 -> Player 1...). You never run out of turns.

Music Playlists: Hitting the "Repeat All" button.

Operating Systems: "Round-robin" scheduling. The CPU gives a tiny slice of time to Google Chrome, then Spotify, then Discord, then loops back to Chrome.