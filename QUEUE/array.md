
```js
class Queue{
    constructor(){
        this.items=[];
    }
    
    enqueue(value){
        this.items.push(value)
    };
    dequeue(){
        if(this.isEmpty()) return 'underflow';
        
        return this.items.shift()
    }
    
    peak(){
        if(this.isEmpty()) return 'underflow';
        return this.items[0]
    };
    print(){
        if(this.isEmpty()) return 'queue is empty';
        let queuestr=''
        for(let i=0;i<this.items.length;i++){
            queuestr+= `${this.items[i]}`+ ' '
            console.log(this.items[i])
            
        }
        console.log(queuestr)
    }
    isEmpty(){
        return this.items.length===0;
    }
}

let x=new Queue();
x.enqueue(10)
x.enqueue(20)
x.enqueue(30)
x.enqueue(40)
x.print()
console.log(x.peak())
```

## Challenge 1: The Printer Spooler (Easy)
* Whenever you send a document to a printer, it goes into a queue. If the printer is busy, the document waits its turn.

* Your Task:
  Write a function called processPrintJobs(jobs) that takes an array of document names. Use your Queue class to load all the documents into the queue, and then simulate printing them one by one until the queue is empty.

```js
  processPrintJobs(["Essay.pdf", "Photo.png", "Resume.docx"]);
// Output:
// Printing: Essay.pdf
// Printing: Photo.png
// Printing: Resume.docx
// All jobs completed!
```
```js
function processPrintJobs(jobs) {
    const printQueue = new Queue(); // Create a new Queue instance
    
    // 1. Load all jobs into the queue (Enqueue)
    for (let i = 0; i < jobs.length; i++) {
        printQueue.enqueue(jobs[i]);
    }
    
    // 2. Process the queue until it's empty
    // As long as isEmpty() is false, keep looping
    while (!printQueue.isEmpty()) { 
        let currentJob = printQueue.dequeue(); // Remove the first item
        console.log("Printing: " + currentJob);
    }
    
    console.log("All jobs completed!");
}

// Test it:
processPrintJobs(["Essay.pdf", "Photo.png", "Resume.docx"]);
```

## Challenge 2: The "Hot Potato" Game (Medium)
* You can simulate a circle using a Queue! To "pass" the potato, you simply dequeue() the person at the front of the line and     immediately enqueue() them back to the end of the line.

* Your Task:
Write a function hotPotato(nameList, num) that takes an array of names and a number (representing how many passes happen before the music stops). Simulate the game using a Queue until only one person is left.

```js
let players = ["John", "Jack", "Camila", "Ingrid", "Carl"];
let winner = hotPotato(players, 7);
console.log("The winner is: " + winner); 
// Hint: The winner should be John.
```
```js
function hotPotato(nameList, num) {
    const queue = new Queue();

    // 1. Put everyone in the queue
    for (let i = 0; i < nameList.length; i++) {
        queue.enqueue(nameList[i]);
    }

    // 2. Keep playing as long as there is more than 1 person left
    // (Note: Since your Queue class exposes the items array, we can check its length)
    while (queue.items.length > 1) {
        
        // Pass the potato 'num' times
        for (let i = 0; i < num; i++) {
            // Remove from front, immediately add to back
            let personToMove = queue.dequeue();
            queue.enqueue(personToMove);
        }
        
        // The loop finished passing. The person at the front is eliminated!
        let eliminated = queue.dequeue();
        console.log(eliminated + " was eliminated.");
    }

    // 3. Only one person is left in the queue, dequeue them as the winner
    return queue.dequeue();
}

// Test it:
let players = ["John", "Jack", "Camila", "Ingrid", "Carl"];
let winner = hotPotato(players, 7);
console.log("The winner is: " + winner);
```

## Challenge 3: The Palindrome Checker (Hard - Combines Stack & Queue)

* Your Task:
Write a function isPalindrome(word) that uses both your Stack class and your Queue class.

* 1. Push every letter of the word into a Stack.

* 2. Enqueue every letter of the word into a Queue.

* 3. Compare the letters as you pop them off the Stack and dequeue them from the Queue. If they all match, it's a palindrome!

```js
console.log(isPalindrome("racecar")); // true
console.log(isPalindrome("javascript")); // false
```
```js
// This assumes you have both your Stack and Queue classes defined in your file!

function isPalindrome(word) {
    const stack = new Stack();
    const queue = new Queue();
    
    // Let's make the word lowercase just to be safe
    let cleanWord = word.toLowerCase();

    // 1. Load every letter into BOTH the Stack and the Queue
    for (let i = 0; i < cleanWord.length; i++) {
        stack.push(cleanWord[i]);
        queue.enqueue(cleanWord[i]);
    }

    // 2. Compare them as we pull them out
    let isPal = true; // We assume it's true until proven false
    
    while (!queue.isEmpty()) {
        let stackLetter = stack.pop();       // Gets letter from the BACK
        let queueLetter = queue.dequeue();   // Gets letter from the FRONT

        // If they don't match even once, it's not a palindrome
        if (stackLetter !== queueLetter) {
            isPal = false;
            break; // Stop the loop early, no need to check the rest
        }
    }
    
    return isPal;
}

// Test it:
console.log("Is 'racecar' a palindrome?", isPalindrome("racecar"));       // true
console.log("Is 'javascript' a palindrome?", isPalindrome("javascript")); // false
```