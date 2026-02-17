## Asymptotic Analysis: Table

```js
Algorithm      Best      TimeAverage   TimeWorst   TimeSpace      Note

Bubble        $O(n)        O(n^2)       O(n^2)       O(1)        Easy, but slow.

Insertion     $O(n)        O(n^2)       O(n^2)       O(1)        Great for nearly sorted data.

Selection    $O(n^2)       O(n^2)       O(n^2)       O(1)        Never use this in production.

Quick       O(n log n)   O(n log n)     O(n^2)     O(\log n)     Fastest in practice usually.

Merge       O(n log n)   O(n log n)   O(n log n)     O(n)        Reliable, stable, but uses memory.
```