# quick sort

- like merge sort -> exploits the fact that arrays of 0 or 1 element are always sorted
- works by selecting one element (called 'pivot') and finding the index where the pivot should end up in the sorted array
  - move all the numbers that are smaller than that number to the left, move all the numbers that are larger than that number to the right
  - not sorted, just shifting them left or right based on pivot
- repeat the process for the left side and then the right side

## pivot helper
- in order to implement quick sort, it's useful to first implement a function responsible for arranging elements in an array on either side of a pivot
- given an array, this helper function should designate an element as the pivot
- it should then rearrange elements in the array so that all values less than the pivot are moved to the left of the pivor, and all values greater than the pivot are moved to the right of the pivot
- the order of elements on either side of the pivot doesn't matter
- the helper should do this **in place**, that is, it shouldn't create a new array
- when complete, the helper should return the index of the pivot

picking a pivot:
- the runtime of quicksort depends in part on how one selects the pivot
- ideally, the pivot should be chosen so that it's roughly the median value in the data set you're sorting
- for simplicity, we'll always choose the pivot to be the first element (will talk about consequences later)

## psuedocode
- write a function called pivot that accepts three arguments
  - an array, a start index, and an end index (these can default to 0 and array length - 1)
- grab the pivot from the start of the array
- store the currect pivot index in a variable (this will keep track of where the pivot shoud end up)
- loop through the array from the start until the end
  - if the pivot is greater than the current element, increment the pivot index variable and then swap the current element with the element at the pivot index
- swap the starting element (ie the pivot) with the pivot index
- return the pivot index

## pivot helper implementation
```js
function pivot(arr, start = 0, end = arr.length + 1) {
  function swap(array, i, j) {
    let temp = array[i];
    array[i] = array[j];
    array[j] = temp;
  }

  let pivot = arr[start];
  let swapIndex = start;

  for (let i = start + 1; i < arr.length; i++) {
    if (pivot > arr[i]) {
      swapIndex++;
      swap(arr, swapIndex, i);
    }
  }
  swap(arr, swapIndex, i);
  return swapIndex;
}
```

## quick sort implementation

psuedocode:
- call the pivot helper on the array
- when the helper returns the updated pivot index, recursively call the pivot helper on the subarray to the left of that index, and the subarray to the right of that index

## implementation
```js
function quickSort(arr, left = 0, right = arr.length - 1) {
  if (left < right) {
    let pivotIndex = pivot(arr, left, right);

     // left
     quickSort(arr, left, pivotIndex - 1);

     // right
     quickSort(arr, pivotIndex + 1, right);
  }
  return arr;
}
```

## bigO

- time complexity:
  - best = O(n log n)
  - average = O(n log n)
  - worst = O(n^2)
- space complexity: O(log n)

similar to merge sort -> as n grows, we have to make log n decompositions. BUT, we also have to make O(n) comparisons in each decomposition

our quicksort starts from the beginning of the array. If the array is already sorted, this would cause the function to make O(n) decompositions and O(n) comparisons per decompositions: O(n^2)
to fix this, we could get around it by making the pivot a random element/middle
- this is why the pivot point makes a difference, depending on the array
