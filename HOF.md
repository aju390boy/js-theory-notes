### Higher order functions

## 1️⃣ map → must return

* **Purpose**: transform items → new array

```js
[1,2,3].map(n => {
  return n * 2;
});

```
# Rule:
* Returned value ➜ goes into the new array
* ❌ No return ➜ undefined is added to the array
* 🧠 Think: "replace each element" 

## 2️⃣ filter → must return boolean

* **Purpose**: select items → new array

```js
[1,2,3,4].filter(n => {
  return n % 2 === 0;
});

```

# Rule:
* true → keep item
* false → remove item
* 🧠 Think: “keep or throw”

## 3️⃣ reduce → must return acc

* **Purpose**: combine all → single value

```js
[1,2,3].reduce((acc, n) => {
  return acc + n;
}, 0);

```


# Rule:
* return acc every time
* returned acc → next iteration acc
* 🧠 Think: “carry forward result”

## 4️⃣ forEach → NO return needed

* **Purpose**: just do something (side effects)

```js

[1,2,3].forEach(n => {
  console.log(n);
});

```

# Rule:
* return ignored
* always returns undefined
* 🧠 Think: “just run code”

## 5️⃣ every → return boolean

* **Purpose**: check all items → true / false

```js

[2,4,6].every(n => n % 2 === 0);

```

# Rule:
* if any false → stops, returns false
* all true → true
* 🧠 Think: “are ALL good?”

## 6️⃣ some → return boolean

* **Purpose**: check at least one → true / false
```js

[1,3,4].some(n => n % 2 === 0);

```


# Rule:
* if any true → stops, returns true
* all false → false
* 🧠 Think: “is ANY good?”