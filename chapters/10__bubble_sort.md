# bubble sort

a sorting algorithm where the largest values bubble up to the top
- as we loop through the array, we compare the element to the next element
- run this over and over until there are no more elements to swap places

in javascript, there are a couple ways of swapping:
```js
function ES5swap(arr, index1, index2) {
  let temp = arr[index1];
  arr[index1] = arr[index2];
  arr[index2] = temp;
}

const ES6swap = (arr, index1, index2) => {
  [arr[index1], arr[index2]] = [arr[index2], arr[index1]];
};
```

## psuedocode

- start looping from the end of the array towards the beginning with a variable called i
- start an inner loop with a variable called j from the beginning until i - 1
- if arr[j] > arr[j + 1] -> swap the two values
- return the sorted array

## implementation

naive solution:
```js
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

the problem with this is that every time the function gets to the end, it compares the last number to undefined. this isn't efficient since it repeatedly does this even though we already know that this is put in the right place

instead, we're going to follow the psuedocode:
```js
function bubbleSort(arr) {
  for (let i = arr.length; i > 0; i--) {
    for (let j = 0; j < i - 1; j++) {     // this way, as i decreases, so does j -> leads to running the loop fewer times
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

## optimization
there's still one more thing we can do to the function to optimize it.

sometimes, the array can be properly sorted _before_ the function can finish looping through all the loops - this takes up unnecessary time
instead, make a check at the end of each loop to see if any swaps were made during that loop. if no, that means the sort is complete
```js
function bubbleSort(arr) {
  let noSwaps;
  for (let i = arr.length; i > 0; i--) {
    noSwaps = true;
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
        noSwaps = false;
      }
    }
    if (noSwaps) break;       // check at end of loop
  }
  return arr;
}
```

## big O complexity

in general, time complexity is O(n^2)
if the data is nearly sorted, best case scenario = O(n)
