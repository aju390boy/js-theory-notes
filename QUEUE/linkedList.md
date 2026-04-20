```js
class Node{
    constructor(value){
        this.value=value;
        this.next=null;
    }
}

class LinkedQueue{
    constructor(){
        this.head=null;
        this.tail=null;
        this.size=0;
    }
    enqueue(val){
        const newNode=new Node(val);
        if(this.isEmpty()){
            this.head=newNode;
            this.tail=newNode;
        }else{
            this.tail.next=newNode;
            this.tail=newNode;
        }
        this.size++;
    }
    dequeue(){
        const newNode= new Node();
        if(this.isEmpty()) return 'list is empty'
        const dequeueNode = this.head;
        this.head=this.head.next;
        this.size--;
        if(this.isEmpty()){
            this.tail=null;
        }
        return dequeueNode.value;
    }
    peak(){
        if(this.isEmpty()) return 'list is empty';
        return this.head.value;
    }
    print(){
        if(this.isEmpty()) return 'list is empty';
        let output='';
        let current=this.head;
        while(current){
            output+=`${current.value} -> `
            current=current.next;
        }
        console.log(output + 'null')
    }
    isEmpty(){
        return this.size===0;
    }
}
const l=new LinkedQueue();
l.enqueue(10)
l.enqueue(30)
l.enqueue(50)
l.enqueue(40)
l.dequeue()
l.dequeue()
console.log(l.peak())
l.print()
```