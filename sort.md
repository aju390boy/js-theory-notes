## Asymptotic Analysis: Table

```js
Algorithm      Best      TimeAverage   TimeWorst   TimeSpace      Note

Bubble        $O(n)        O(n^2)       O(n^2)       O(1)        Easy, but slow.

Insertion     $O(n)        O(n^2)       O(n^2)       O(1)        Great for nearly sorted data.

Selection    $O(n^2)       O(n^2)       O(n^2)       O(1)        Never use this in production.

Quick       O(n log n)   O(n log n)     O(n^2)     O(\log n)     Fastest in practice usually.

Merge       O(n log n)   O(n log n)   O(n log n)     O(n)        Reliable, stable, but uses memory.
```

# 4. Quick Sort

### "Divide and Conquer." Pick a Pivot (a leader). Throw everyone smaller to the Left, everyone bigger to the Right. Now you have   two smaller arrays. Do the same thing to them. Repeat until the arrays are tiny.

```js

function quickSort(arr) {
    // Base Case: If array has 0 or 1 items, it is already sorted
    if (arr.length <= 1) {
        return arr;
    }

    // 1. Pick a pivot (We'll use the last element here)
    let pivot = arr[arr.length - 1];
    
    // 2. Create left and right arrays
    let left = [];
    let right = [];

    // 3. Partition: Loop through everything EXCEPT the pivot
    for (let i = 0; i < arr.length - 1; i++) {
        if (arr[i] < pivot) {
            left.push(arr[i]); // Smaller goes left
        } else {
            right.push(arr[i]); // Bigger goes right
        }
    }

    // 4. Recursion: Sort left, Sort right, and combine them with pivot in middle
    // spread operator (...) expands the arrays
    return [...quickSort(left), pivot, ...quickSort(right)];
}

console.log(quickSort([8, 2, 4, 7, 1, 3, 9, 6, 5]));

```

## Q. Does recursion happen only once, or does it depend on the array's length?

### Answer: It happens many times. It happens over and over again until the array cannot be split anymore.

### Think of it like Russian Nesting Dolls (Matryoshka dolls) or Opening Boxes.

### 1. You have a big box (the full array). You open it, take out the "Pivot," and find two smaller boxes inside (left and right).
### 2. You cannot finish the job until you open those smaller boxes.
### 3. When you open the left box, you find even smaller boxes inside that one.
### 4. You keep opening boxes until you find a box with only 0 or 1 item. That box is "done."

## Visual Walkthrough: [8, 2, 4, 7, 1, 3, 9, 6, 5]
### Let's trace exactly what happens to your array. To make it easier to read, I will use indentation to show "inside a box."

## Step 1: The Big Call (Level 0)

* Array: [8, 2, 4, 7, 1, 3, 9, 6, 5]

* Pivot: 5 (The last item)

* Sorting:
 Smaller than 5 (left): [2, 4, 1, 3]
 Bigger than 5 (right): [8, 7, 9, 6]

* The Code pauses here: It waits for quickSort([2, 4, 1, 3]) to finish.
  Current Goal: [...Wait for Left, 5, ...Wait for Right]

  ## Step 2: Solving the Left Side (Level 1)

* Array: [2, 4, 1, 3]

* Pivot: 3

* Sorting:
  Smaller than 3 (left): [2, 1]
  Bigger than 3 (right): [4]

* The Code pauses here: It waits for quickSort([2, 1]).
  Current Goal: [...Wait for Left, 3, ...Wait for Right]

  ## Step 3: Deeper into the Left Side (Level 2)

  ### Array: [2, 1]
  ### Pivot: 1
  ### Sorting:
  * Smaller than 1 (left): [] (Empty)
  * Bigger than 1 (right): [2]
  ### Action:
  * quickSort([]) returns [] immediately (Base Case).
  * quickSort([2]) returns [2] immediately (Base Case).
  ### Result: The function glues them together: [[], 1, [2]] $\rightarrow$ [1, 2]

  ## Step 4: Back up to Level 1
  ### Now we have the answer for the "Left Side" of Step 2!
  ### We know Left is [1, 2].
  ### We know Pivot was 3.
  ### We know Right was [4].
  ### Result: [[1, 2], 3, [4]] $\rightarrow$ [1, 2, 3, 4]

  ## Step 5: Solving the Right Side (Level 1)
  ### Remember Step 1? We were waiting for the Right side [8, 7, 9, 6].
  ### Array: [8, 7, 9, 6]
  ### Pivot: 6
  ### Sorting:
  * Smaller than 6 (left): [] (Nothing is smaller!)
  * Bigger than 6 (right): [8, 7, 9]
  ### The Code pauses: Waits for quickSort([8, 7, 9]).

  ## Step 6: Deeper into the Right Side (Level 2)
  ### Array: [8, 7, 9]
  ### Pivot: 9
  ### Sorting:
  * Smaller (left): [8, 7]
  * Bigger (right): []
  ### The Code pauses: Waits for quickSort([8, 7]).

  ## Step 7: Deepest Right Side (Level 3)
  ### Array: [8, 7]
  ### Pivot: 7
  ### Sorting:
      * Left: []
      * Right: [8]
  ### Result: [[], 7, [8]] $\rightarrow$ [7, 8]

###  Step 8: Folding it all back together
Now the answers "bubble up" (return) to the top.

* 1. From Step 7: The array [8, 7, 9] becomes $\rightarrow$ [7, 8, 9]
* 2. From Step 5: The array [8, 7, 9, 6] becomes [[], 6, [7, 8, 9]] $\rightarrow$ [6, 7, 8, 9]
* 3. Back to Step 1 (The Big Start):
    * We have the sorted Left: [1, 2, 3, 4]
    * We have the Pivot: 5
    * We have the sorted Right: [6, 7, 8, 9]

## Final Code Execution:

```js
return [...[1, 2, 3, 4], 5, ...[6, 7, 8, 9]];
// Result: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
## Summary

* Recursion runs many times: It creates a "tree" of calls.
* It pauses: The main function literally stops and waits for the "children" functions to finish sorting their tiny lists.
* It reassembles: The final sorted list is built by gluing together many tiny sorted lists.

## Method 2

```js
// arr: the array we are sorting
// low: the starting index of the chunk we are looking at
// high: the ending index of the chunk we are looking at
function quickSortPro(arr, low = 0, high = arr.length - 1) {
  
  // Base Case: If low is NOT less than high, it means our chunk has 
  // 1 or 0 items. A chunk of 1 item is already sorted!
  if (low < high) {
    
    // PARTITION: This is the heavy lifter. 
    // It picks a pivot, puts smaller stuff left, bigger stuff right,
    // and returns the EXACT final index where the pivot landed.
    const pivotIndex = partition(arr, low, high);
    
    // RECURSION: Now sort the left chunk (everything before the pivot)
    quickSortPro(arr, low, pivotIndex - 1);
    
    // RECURSION: And sort the right chunk (everything after the pivot)
    quickSortPro(arr, pivotIndex + 1, high);
  }

  // Return the same array we started with (it is now modified/sorted)
  return arr;
}

// The Swapping Function
function partition(arr, low, high) {
  // 1. Pick the last item in our chunk as the Boss (Pivot)
  const pivot = arr[high];
  
  // 2. 'i' is our tracker for the "smaller numbers" club.
  // It starts exactly one step BEFORE our chunk begins.
  let i = low - 1;

  // 3. 'j' scans through the chunk from left to right
  for (let j = low; j < high; j++) {
    
    // 4. If we find a number smaller than our Boss...
    if (arr[j] < pivot) {
      i++; // Move our "smaller numbers" tracker forward
      
      // SWAP: Trade the places of the item at 'i' and the item at 'j'
      // This throws the smaller number to the left side!
      [arr[i], arr[j]] = [arr[j], arr[i]]; 
    }
  }

  // 5. The loop is done. All smaller numbers are on the left.
  // Now, put the Boss (pivot) right after the last small number.
  [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];

  // 6. Tell the main function exactly where the Boss landed.
  return i + 1;
}
```