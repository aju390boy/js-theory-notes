# STACK


##  Stack using Array

```js
class Stack{
    constructor(){
        this.items=[];
    }
    
    push(value){
        this.items.push(value);
    }
    pop(){
        if(this.isEmpty()) return 'underflow';
        return this.items.pop()
    }
    peak(){
        if(this.isEmpty()) return 'underflow';
        
        return this.items[this.items.length-1]
    };
    print(){
        if(this.isEmpty()) return 'underflow';
        for(let i=0;i<this.items.length;i++){
            console.log(this.items[i])
        }
    }
    isEmpty(){
        return this.items.length===0;
    }
}
const item1=new Stack();
item1.push(10)
item1.push(40)
item1.push(30)
item1.push(20)
item1.pop()
console.log(item1.peak())
```

## Reverse a String

```js

function reverseString(str){
    let stack=[];
    let reversedString='';
    for(i=0;i<str.length;i++){
        stack.push(str[i])
    }
    
    while(stack.length>0){
        reversedString+=stack.pop()
    }
    return reversedString;
}

console.log(reverseString("JavaScript"));

```

## reverse stack using reccursion

```js

function reverse(stack){
    if(stack.isEmpty()) return
    let temp = stack.pop()
    reverse(stack)
    insert(stack, temp)
}

function insert(stack, x){
    if(stack.isEmpty()) {
        stack.push(x)
        return 
    }
    let temp = stack.pop()
    insert(stack, x)
    stack.push(temp)
}

```

## Valid Parentheses

```js
function isValid(s) {
  const stack = [];
  const map = {
    ')': '(',
    '}': '{',
    ']': '['
  };

  for (let char of s) {
    if (map[char]) {
      // It's a closing bracket
      const topElement = stack.length === 0 ? '#' : stack.pop();
      if (topElement !== map[char]) return false;
    } else {
      // It's an opening bracket
      stack.push(char);
    }
  }
  return stack.length === 0;
}

console.log(isValid("({[]})")); // true
console.log(isValid("([)]"));   // false

```