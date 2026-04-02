```js

class Hash{
    constructor(size){
        this.size =size
        this.table = new Array(size)
    }
    hash(key){
        if(typeof key === 'number'){
            return key%this.size
        }
        if(typeof key === 'string') {
            let total = 0
            for(let i=0;i<key.length;i++){
                total += key.charCodeAt(i)
            }
            return total%this.size
        }
    }
    set(key,val){
        let ind = this.hash(key)
        while(this.table[ind] !== undefined && this.table[ind].key !== key) {
            ind = (ind+1)%this.size
        }
        this.table[ind] = {key,val}
    }
    get(key) {
        let ind = this.hash(key)
        while(this.table[ind] !== undefined){
            if(this.table[ind].key === key) {
                return this.table[ind].val
            }
            ind = (ind+1)%this.size
        }
    }
    remove(key) {
        let ind = this.hash(key)
        while(this.table[ind] !== undefined) {
            if(this.table[ind].key === key) {
                this.table[ind] = undefined
            }
            ind = (ind+1)%this.size
        }
    }
    print(){
        for(let i=0;i<this.table.length;i++){
            if(this.table[i]) {
                console.log(i, this.table[i])
            }
        }
    }
}
const h = new Hash(5)
h.set('name','ajith')
h.set('nama','anagha')
h.set(20,'manu')

h.print()
```