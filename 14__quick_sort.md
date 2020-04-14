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

