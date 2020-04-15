# selection sort

similar to bubble sort, but instead of first placing large values into sorted position, it places small values into sorted position

like, going through to find a minimum, and after a round of comparisons put that minimum at the front

## psuedocode
- store the first element as the smallest value you've seen so far
- compare this item to the next item in the array until you find a smaller number.
- if a smaller number is found, designate that smaller number to be the new minimum and continue until the end of the day
- if the minimum is not the value (index) you initially began with, swap the two values
- repeat this with the next element until the array is sorted

## implementation

```js
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let lowest = i;
    for (let j = i + 1; j <  arr.length; j++) {
      if (arr[j] < arr[lowest]) {
        lowest = j;
      }
    }
    if (i !== lowest) {
      //swap
      let temp = arr[i];
      arr[i] = arr[lowest];
      arr[lowest] = temp;
    }
  }
  return arr;
}
```

## big O complexity
 time complexity = O(n^2)

 there IS one scenario where selection sort can be better than bubble sort, which is if you're in a situation where you want to minimize the number of swaps you're making
 - in bubble sort, you're constantly swapping
 - in selection sort, you're only swapping at the end of each loop

