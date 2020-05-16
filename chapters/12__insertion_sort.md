# insertion sort

builds up the sort by gradually creating a larger left half which is always sorted
- instead of finding the largest/smallest element at a time, it takes each element and places it where it should go in the sorted portion of the array

eg.

```js
  [5, 3, 4, 1, 2]
// o  ^
  [3, 5, 4, 1, 2]
// o..o  ^
  [3, 4, 5, 1, 2]
// o.....o  ^
  [1, 3, 4, 5, 2]
// o........o  ^
  [1, 2, 3, 4, 5]
```

## psuedocode
- start by picking the second element in the array
- now compare the second element with the one before it and swap if necessary
- continue to the next element and if it is in the incorrect order, iterate through the sorted portion to place the element in the correct place
- repeat until the array is sorted

## implementation
```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let currentVal = arr[i];
    for (let j = i - 1; j >= 0 && arr[j] > currentVal; j--) {
      arr[j + 1] = arr[j];
    }
    arr[j + 1] = currentVal;
  }
  return arr;
}
```

## big O notation
time complexity = O(n^2)

online algorithm: an algorithm that can work as it receives new data, it doesn't have to have it all at once
- with insertion sort, because we're keeping one side of the array sorted and we're inserting items one at a time, it doesn't matter what data comes in because we can place it where it needs to go

