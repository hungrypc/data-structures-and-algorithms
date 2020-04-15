all the sorting algorithms we've seen so far are called comparison sorts -> the base comparison that we're doing is between two items at any given point

the fastest we can ever really get with comparison sorts is O(n log n).

so are there any faster sorting algorithms? sort of, but not through comparisons
- these algorithms take advantage of certain properties of the data

# radix sort

a special sorting algorithm that works on lists of numbers
- it never makes comparisons between elements
- instead, it exploits the fact that information about the size of a number is encoded in the number of digits
- more digits means bigger number

this sort looks at the numbers digit by digit (from right to left) and puts them into buckets (from 0 - 9) - process is repeated for each digit (number of times this happens depends on the number with the largest number of digits) until the list is completely sorted

## helper methods
in order to implement radix sort, it's helpful to build a few helper function first:

getDigit(num, place) = returns the digit in _num_ at the given _place_ value
```js
function getDigit(num, i) {
  return Math.floor(Math.abs(num) / Math.pow(10, i)) % 10;
}
```

digitCount(num) = returns th number of digits in _num_
```js
function digitCount(num) {
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}
```

mostDigits(nums) = given an array of numbers, returns the number of digits in the largest numbers in the list
```js
function mostDigits(nums) {
  let maxDigits = 0;
  for (const n of nums) {
    maxDigits = Math.max(maxDigits, digitCount(n));
  }
  return maxDigits;
}
```

## psuedocode

- define a function that accepts a list of numbers
- figure out how many digits the largest number has
- loop from k = 0 up to this largest number of digits
- for each iteration of the loop:
  - create buckets for each digit (0 to 9)
  - place each number in the corresponding bucket based on its kth digit
- replace our existing array with values in our buckets, starting with 0 and going up to 9
- return list at the end

## implementation
```js
function radixSort(nums) {
  let maxDigitCount = mostDigits(nums);

  for (let k = 0; k < maxDigitCount; k++) {
    let digitBuckets = Array.from({length: 10}, () => []); // creates an array of 10 empty arrays
    for (let i = 0; i < nums.length; i++) {
      let digit = getDigit(nums[i], k);
      digitBuckets[digit].push(nums[i]);
    }
    nums = [].concat(...digitBuckets);
  }
  return nums;
}
```


## big O

n = number of things we're sorting
k = length of those numbers

- time complexity:
  - best = O(nk)
  - average = O(nk)
  - worst = O(nk)
- space complexity = O(n + k)

this is a lil controversial though... there are two arguments about the time complexity
- if you're dealing with all unique numbers, then k simplifies to log n, making the bigO = O(n log n)
  - makes this only equally as good as comparison sorts
- not sure about the counter argument, go read the wiki and come back to this
