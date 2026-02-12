# Linked List

## 1. The Building Block: class Node
### Think of a Node as one single train car. It holds some cargo (data) and has a hook to connect to the next car.

```js
class Node {
  constructor(value) {
    this.value = value;  // The Cargo: The actual number we want to store (e.g., 10)
    this.next = null;    // The Hook: Points to the next train car. Initially, it's not connected to anything (null).
  }
}
```
* class Node: We are defining a blueprint for a "Node".

* constructor(value): This runs when we say new Node(10). It sets up the new block.

* this.value = value: Saves the data (like 10) inside the block.

* this.next = null: By default, this block isn't holding onto anyone else yet. null means "nothing".


## 2. The Manager: class LinkedList
### This is the Train Station Master. It doesn't hold the data itself; it just knows where the first train car (the head) is.

```js
class LinkedList {
  constructor() {
    this.head = null; // The start. At the beginning, there are no cars, so the head is empty (null).
    this.size = 0;    // A counter to keep track of how many items we have. Starts at 0.
  }

  isEmpty() { return this.size === 0; } // A simple helper to ask: "Is the list empty?"
}

  ```
  * this.head: This is the most important variable. It points to the first node. If we lose the head, we lose the whole list!

## 3. Adding to the End: append(value)
### This acts like: "Go find the end of the line and attach this new guy."

```js
append(value) {
    const node = new Node(value); // 1. Create a new node (train car) with the value.
    
    if (this.isEmpty()) {         // 2. Is the parking lot empty?
      this.head = node;           //    If yes, this new node becomes the HEAD (the first one).
    } else {
      
      // 3. The list is NOT empty. We need to walk to the end.
      let current = this.head;    //    Start at the beginning (head).
      
      while (current.next) {      //    Loop: "Does the current car have a 'next' car attached?"
        current = current.next;   //    Yes? Then move to that next car. Keep going until we find the last one.
      }
      
      current.next = node;        // 4. We found the last car! Attach our new node to its 'next'.
    }
    this.size++;                  // 5. Increase the counter. We have one more item.
  }

  ```
  * current: Think of this as your finger pointing at a node. You move your finger from one node to the next until you hit the end.

## 4. Adding to the Front: prepend(value)
### This is easier. We just push everyone back and put the new guy at the very front.

```js
prepend(value) {
    const node = new Node(value); // 1. Create the new node.
    
    node.next = this.head;        // 2. Point the NEW node's hook to the CURRENT head (the old first guy).
    this.head = node;             // 3. Now, update the official HEAD pointer to be our NEW node.
    
    this.size++;                  // 4. Increase the counter.
  }

  ```

  * Why is this fast? We don't need a loop! We don't need to walk to the end. We just swap the first spot.

## 5. Deleting: removeValue(value)
### his is the trickiest part. To remove a guy in the middle, we have to find the guy before him and tell him to skip the guy we are deleting.

```js
removeValue(value) {
    if (this.isEmpty()) return null; // If list is empty, we can't delete anything. Exit.

    // SCENARIO 1: We want to delete the HEAD (the very first guy).
    if (this.head.value === value) {
      this.head = this.head.next;    // Make the SECOND guy the new HEAD. The old first guy is now lost/deleted.
      this.size--;                   // Decrease count.
      return value;                  // Done.
    }

    // SCENARIO 2: We want to delete someone in the middle or end.
    let current = this.head;         // Start at the front.
    
    // The Loop: We look AHEAD. We check if the NEXT guy exists, and if the NEXT guy is the one we want to kill.
    // We stop looping if we reach the end OR if we find the guy.
    while (current.next && current.next.value !== value) {
      current = current.next;        // Move forward.
    }

    // After the loop, did we find him?
    if (current.next) {              // If 'current.next' is not null, it means we found the target!
      current.next = current.next.next; // THE MAGIC: Change the hook to SKIP the target node and point to the one after it.
      this.size--;
      return value;
    }
    
    return null; // We went through the whole list and didn't find that value.
  }

  ```

### The Key Logic: current.next = current.next.next.

* magine Node A -> Node B -> Node C.

* We want to delete B.

* We stand on A (current).

* We change A's pointer (current.next) to skip B and point straight to C (current.next.next).

* B is now detached and floating in space (garbage collected).

## 6. Showing the List: print()
### We just walk through the list and add the numbers to a string.

```js
print() {
    if (this.isEmpty()) {
      console.log("List is empty");
    } else {
      let current = this.head;    // Start at head.
      let output = "";            // Create a blank string to hold the answer.
      
      while (current) {           // While 'current' is a real node (not null)...
        output += `${current.value} -> `; // Add the value to our string.
        current = current.next;           // Move to the next node.
      }
      
      console.log(output + "null"); // Print it out, adding "null" at the end to show where it stops.
    }
  }

  ```

# PRACTICAL QUESTIONS


### Question 1: Reverse the Linked List
The Goal: Turn 1 -> 2 -> 3 -> null into 3 -> 2 -> 1 -> null.

The Logic (Noob English): Imagine a line of people holding hands. Person A holds B's hand. B holds C's hand. To reverse it, you have to tell everyone to let go of the person in front of them and grab the hand of the person behind them. We need three pointers to do this safely so we don't lose anyone:

* prev: The person behind you (starts as null/empty).

* current: The person we are currently dealing with.

* next: The person ahead (we need to remember them before we let go!).

```js

reverse() {
    let prev = null;
    let current = this.head;
    
    while (current) {
        const nextNode = current.next; // 1. Save the next guy so we don't lose him
        current.next = prev;           // 2. Turn the arrow backward! Point to 'prev'
        
        // 3. Move everyone forward one step
        prev = current;                
        current = nextNode;
    }
    
    this.head = prev; // 4. Reset the head to the last node we touched
}

```
### Question 2: Find the Middle Node
The Goal: Find the center value in one pass. Input: 1 -> 2 -> 3 -> 4 -> 5 Output: 3

* The Logic (The Tortoise and the Hare): Imagine a race track. You have two runners:

* Tortoise (Slow): Runs 1 step at a time.

* Hare (Fast): Runs 2 steps at a time.

When the Hare reaches the finish line (the end of the list), the Tortoise will be exactly halfway there!

```js

findMiddle() {
    let slow = this.head;
    let fast = this.head;

    // While the Hare still has track to run on (must check fast AND fast.next)
    while (fast && fast.next) {
        slow = slow.next;       // Run 1 step
        fast = fast.next.next;  // Run 2 steps
    }

    return slow.value; // Slow is now standing in the middle
}

```

### Question 3: Remove Duplicates

```js
removeDuplicates() {
    let seen = new Set();
    let current = this.head;
    let prev = null;

    while(current){
        if(seen.has(current.value)){
            // remove node
            prev.next = current.next;
            this.size--;
        }else{
            seen.add(current.value);
            prev = current;
        }
        current = current.next;
    }
}

```

### Question 3: Remove Duplicates (From Sorted List)
The Goal: Delete repeated numbers. Input: 1 -> 1 -> 2 -> 3 -> 3 Output: 1 -> 2 -> 3

* The Logic: Since the list is sorted, duplicates are always neighbors. We look at the current node and ask: "Is my value the same as the next guy's value?"

* Yes: Skip the next guy (current.next = current.next.next).

* No: Just move forward normally.

```js

removeDuplicates() {
    let current = this.head;

    while (current && current.next) {
        if (current.value === current.next.value) {
            // They are twins! Skip the next one.
            current.next = current.next.next;
            this.size--; // Don't forget to decrease size!
        } else {
            // Neighbors are different, move forward.
            current = current.next;
        }
    }
}

```