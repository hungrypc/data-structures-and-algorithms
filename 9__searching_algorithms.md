# searching algorithms

## linear search
looking through list one by one from start to finish
- time complexity = O(n);

## binary search
- much faster form of search
- rather than eliminating one element at a time, you can eliminate _half_ of the remaining elements at a time
- only works on _sorted_ arrays

the idea is divide and conquer: split the array into two pieces, pick a pivot point (usually the middle) and search left side or right side - depending on the condition, we can eliminate the left or the right

```js
function binarySearch(arr, n) {
  let start = 0;
  let end = arr.length - 1;
  let middle = Math.floor((start + end) / 2);

  while (arr[middle] !== n && start <= end) {
    if (arr[middle] > n) {
      end = middle - 1;
    } else {
      start = middle + 1;
    }
    middle = Math.floor((start + end) / 2);
  }
  return arr[middle] === n ? middle : -1;
}
```

binary search bigO:
- best case = O(1)
- worst and average case = O(log n)


## naive string search

write a function that counts the number of times a smaller string appears in a longer string

```js
function naiveSearch(long, short) {
  let count = 0;
  for (let i = 0; i < long.length; i++) {
    for (let j = 0; j < short.length; j++) {
      if (short[j] !== long[i + j]) break; // break out of inner loop
      if (j === short.length - 1) count++;
    }
  }
}
```