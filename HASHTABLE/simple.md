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

## Questions 

* Two Sum
```js
function prime(nums,target){
    const map=new Map();
    for(let i=0;i<nums.length;i++){
        const value= target-nums[i];
        if(map.has(value)){
            return [map.get(value),i];
        }
        map.set(nums[i],i)
    }
    return [];
}
let nums=[3,2,6,8]
console.log(prime(nums,7))
```

* First Non-Repeating Character
```js
function firstUniqChar(s) {
  const frequencyMap = {};

  // Build frequency map
  for (let char of s) {
    frequencyMap[char] = (frequencyMap[char] || 0) + 1;
  }

  // Find the first char with count 1
  for (let i = 0; i < s.length; i++) {
    if (frequencyMap[s[i]] === 1) {
      return i;
    }
  }

  return -1;
}

// Test
console.log(firstUniqChar("javascriptisawesome")); // 0 (j)
console.log(firstUniqChar("aabb")); // -1
```

* Group Anagrams
```js
function groupAnagrams(strs) {
  const groups = new Map();

  for (let str of strs) {
    // Sort string to create a uniform key
    const sortedKey = str.split('').sort().join('');
    
    if (!groups.has(sortedKey)) {
      groups.set(sortedKey, []);
    }
    
    groups.get(sortedKey).push(str);
  }

  return Array.from(groups.values());
}

// Test
const words = ["eat", "tea", "tan", "ate", "nat", "bat"];
console.log(groupAnagrams(words)); 
// [["eat","tea","ate"],["tan","nat"],["bat"]]
```