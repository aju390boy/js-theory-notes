## Asymptotic Analysis: Table

```js
Algorithm      Best      TimeAverage   TimeWorst   TimeSpace      Note

Bubble        $O(n)        O(n^2)       O(n^2)       O(1)        Easy, but slow.

Insertion     $O(n)        O(n^2)       O(n^2)       O(1)        Great for nearly sorted data.

Selection    $O(n^2)       O(n^2)       O(n^2)       O(1)        Never use this in production.

Quick       O(n log n)   O(n log n)     O(n^2)     O(\log n)     Fastest in practice usually.

Merge       O(n log n)   O(n log n)   O(n log n)     O(n)        Reliable, stable, but uses memory.
```

## Selection vs Bubble

### 👉 2 loops,O(n²), simple logic , But internally… totally different mindset.

* 🟡 Bubble Sort
“Push the largest element to the end step by step”
Each round : Compare adjacent elements,Swap if wrong
Too many swaps
best case : O(n) if already sorted
but bubble sort is more stable

* 🔵 Selection Sort
“Find the smallest element and place it at correct position”
Each round : Find minimum,Swap once
Minimum swaps (only one per round)
best case : Still O(n²)
selection sort not stable bt perfomance wise good