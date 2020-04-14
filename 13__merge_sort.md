# merge sort

- its a combination of two things - merging and sorting
- exploits the fact that arrays of 0 or 1 element are always sorted
- works by decomposing an array into smaller arrays of 0 or 1 elements, then building up a newly sorted array

## psuedocode (semi)
note:
- in order to implement merge sort, it's useful to first implement a function responsible for merging two sorted arrays
- given two sorted arrays, this helper function should create a new array which is also sorted, and consists of all of the elements in the two input arrays
- this function should run in **O(n+m)** time and **O(n+m)** space and **should not** modify the parameters passed to it
  - this means that we're iterating over each item in each array _once_

psuedo:
- create an empty array, take a look at the smallest values in each input array
- have two counters (use while loops) that start at 0
- while there are still values we haven't looked at
  - if the value in the first array is smaller than the value in the second array, push the value in the first array into our results and move on to the next value in the first array
  - if the value in the first array is larger than the value in the second array, push the value in the second array into our results and move on  to the next value in the second array
  - once we exhaust one array, push in all remaining values from the other array

## implementation (semi)

```js
function merge(arr1, arr2) {
  let results = [];
  let i = 0;
  let j = 0;
  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) {
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }

  while (i < arr1.length) {
    results.push(arr1[i]);
    i++;
  }

  while (j < arr2.length) {
    results.push(arr2[j]);
    j++;
  }

  return results;
}
```

## mergeSort psuedocode

- break up the array into halves until you have arrays that are empty or have one element (use slice)
- once you have smaller sorted arrays, merge those arrays with other sorted arrays until you are back at the full length of the array
- once the array has been merged back together, return the merged (and sorted) array

## writing mergeSort

```js
function merge(arr1, arr2) {
  let results = [];
  let i = 0;
  let j = 0;
  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) {
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }

  while (i < arr1.length) {
    results.push(arr1[i]);
    i++;
  }

  while (j < arr2.length) {
    results.push(arr2[j]);
    j++;
  }

  return results;
}

function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  let mid = Math.floor(arr.length / 2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));

  return merge(left, right);
}
```

































