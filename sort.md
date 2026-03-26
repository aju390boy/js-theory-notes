# Asymptotic Analysis: Table

```js
Algorithm      Best      TimeAverage   TimeWorst   TimeSpace      Note

Bubble        $O(n)        O(n^2)       O(n^2)       O(1)        Easy, but slow.

Insertion     $O(n)        O(n^2)       O(n^2)       O(1)        Great for nearly sorted data.

Selection    $O(n^2)       O(n^2)       O(n^2)       O(1)        Never use this in production.

Quick       O(n log n)   O(n log n)     O(n^2)     O(\log n)     Fastest in practice usually.

Merge       O(n log n)   O(n log n)   O(n log n)     O(n)        Reliable, stable, but uses memory.
```

# Selection vs Bubble


### 🟡 Bubble Sort
* “Push the largest element to the end step by step”
* Each round : Compare adjacent elements,Push biggest to the end each round,Too much unnecessary movement
* Too many swaps
* best case : O(n) if already sorted
* but bubble sort is more stable

### 🔵 Selection Sort
* “Find the smallest element and place it at correct position”
* Each round : Find minimum,Swap once
* Minimum swaps (only one per round)
* best case : Still O(n²)
* selection sort not stable bt perfomance wise good

### Insertion Sort
* “Take one element and place it in the correct position”
* Like arranging cards in your hand 🃏
* Mostly shifting,Shift elements to insert at correct spot
* best case : O(n) if already sorted
* Very fast for small arrays,stable,perfomence

### Quick Sort
* Quick Sort uses divide and conquer
* Instead of comparing everything again and again like bubble sort…
* It splits the array into smaller parts,Solves each part independently
* Choose pivot,Put smaller left, bigger right,No merging needed
* Quick sort doesn’t need extra arrays (mostly),Less memory usage,Faster in real systems
* Quick sort is NOT always fast,Quick sort is fast only when it divides well
* Worst case : O(n²),(Array already sorted,Bad pivot choice(first or last)),Reverse sorted array
* O(n log n) : n → n/2 → n/4 → n/8 ...
* Use random pivot to avoid worst case

```js
[5,3,1,4]

pivot = 4

Left  → [3,1]
Right → [5]

Then repeat...
```

### Merge Sort 
* Merge Sort uses divide and conquer
* “Divide → sort → then MERGE” 
* Split array into halves,Sort both sides,Combine (merge)
* merge sort always O(n log n)
* Merge sort is consistent,stable,predictable performance
* Uses extra memory (new arrays)

```js
[5,3,1,4]

Split:
[5,3]   [1,4]

Split again:
[5][3]  [1][4]

Merge:
[3,5]   [1,4]

Final merge:
[1,3,4,5]
```

Quick sort is faster in practice due to in-place sorting and better cache performance, but merge sort guarantees O(n log n) and is stable, making it better when consistency or stability is required.”