# problem solving patterns

## frequency counter

_using **objects or sets** to collect values/frequencies of values_
- this can often avoid the need for nested loops or O(n^2) operations with arrays/strings

eg. write a function called **same**, which accepts two arrays. the function should return true if every value in the array has it's corresponding value squared in the second array. the frequency of values must be the same
```js
same([1, 2, 3], [4, 1, 9]); // true
same([1, 2, 3], [1, 9]);    // false
same([1, 2, 1], [4, 4, 1]); // false (must be same frequency)
```

solution:
```js
function same(arr1, arr2) {
  if (arr1.length !== arr2.length) {
    return false;
  }
  let frequencyCount1 = {};
  let frequencyCount2 = {};
  for (let val of arr1) {
    frequencyCount1[val] = (frequencyCount1[val] || 0) + 1;
  }
  for (let val of arr2) {
    frequencyCount2[val] = (frequencyCount2[val] || 0) + 1;
  }
  for (let key in frequencyCount1) {
    if (!(key ** 2 in frequencyCount2)) {
      return false;
    }
    if (freqCoun2[key ** 2] !== frequencyCount1[key]) {
      return false;
    }
  }
  return true;
}
````

time complexity = O(n)
space complexity = O(n)

practice question:
given two strings, write a function to determine if the second string is an anagram of the first. an anagram is a word formed by rearranging the letters of another
```js
validAnagram('', ''); // true
validAnagram('aaz', 'zza'); // false
validAnagram('anagram', 'nagaram'); // true
```

i know that an anagram means that there should be the same amount of each letters in both words. i can use a frequency counter to map out the letter count of each word and compare. if letter counts are equal, return true. else, false.

```js
function validAnagram(str1, str2) {
  let count1 = {};
  let count2 = {};
  for (const i of str1) {
    count1[i] = (count1[i] || 0) + 1;
  }
  for (const j of str2) {
    count2[j] = (count2[j] || 0) + 1;
  }
  for (const letter in count1) {
    if (count1[letter] !== count2[letter]) {
      return false;
    }
  }
  return true;
}
```
could do better and reduce space by only having one map rather than two:
```js
function validAnagram(str1, str2) {
  if (str1.length !== str2.length) {
    return false;
  }
  let lookup = {};
  for (const letter of str1) {
    lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
  }
  for (const letter of str2) {
    if (!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }
  return true;
}
```
time complexity = O(n)
space complexity = O(n)


## multiple pointers

_creating **pointers** of values that correspond to an index/position and move towards the beginning, end, or middle based on a certain condition_
- **very** efficient for solving problems with minimal space complexity

eg. write a function called sumZero which accepts a sorted array of integers. the function should find the first pair where the sum is 0. return an array that includes both values that sum to zero or undefined if a pair does not exist

```js
sumZero([-3, -2, -1, 0, 1, 2, 3]); // [-3, 3]
sumZero([-2, 0, 1, 3]); // undefined
sumZero([1, 2, 3]); // undefined
```

solution:
```js
function sunZero(arr) {
  let left = 0;               // pointer 1
  let right = arr.length - 1; // pointer 2
  while (left < right) {
    let sum = arr[left] + arr[right];
    if (sum === 0) {
      return [arr[left], arr[right]];
    } else if (sum > 0) {
      right --;
    } else {
      left ++;
    }
  }
}
````

time complexity = O(n)
space complexity = O(1)

practice question:
implement a function called countUniqueValues, which accepts a sorted array, and counts the unique values in the array. there can be negative number sin the array, but it will always be sorted
```js
countUniqueValues([1, 1, 1, 1, 1, 2]); // 2
countUniqueValues([1, 2, 3, 4, 4, 4, 7, 7, 12, 12, 13]); // 7
countUniqueValues([]); // 0
countUniqueValues([-2, -1, -1, 0, 1]); // 4
```

since the array will always be sorted, i can count on the fact that duplicates will always be next to the first instance of that number. using two pointers, ill have the second pointer placed on i + 1, where i will be the index of the first pointer. if pointer 1 !== pointer 2, count ++ and move pointer 1 up by 1. if pointer 1 === pointer 2, move pointer 1 up by 1.

```js
function countUniqueValues(arr) {
  let count = 0;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== arr[i + 1]) {
      count++;
    }
  }
  return count;
}
```
time complexity = O(n)
space complexity = O(1)


## sliding window

_creating a **window** which can either be an array or number from one position to another_

depending on a certain condition, the window either incrases or closes (and a new window is created)
- useful for keeping track of a subset of data in an array/string/etc

eg. write a function that accepts a string and finds the longest sequence of unique characters

eg. write a function called maxSubarraySum which accepts an array of integers and a number called n. the function should calculate the maximum sum of n consecutive elements in the array

```js
maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 2); // 10
maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 4); // 17
maxSubarraySum([4, 2, 1, 6], 1); // 6
maxSubarraySum([4, 2, 1, 6, 2], 1); // 13
maxSubarraySum([], 4); // null
```

solution:
```js
function maxSubarraySum(arr, num) {
  let maxSum = 0;
  let tempSum = 0;
  if (arr.length < num) return null;
  for (let i = 0; i < num; i++) {
    maxSum += arr[i];
  }
  tempSum = maxSum;
  for (let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum);
  }
  return maxSum;
}
```
explanation:
instead of re-adding numbers that have already been added together, subtract the window's first element's value and add the remainder to the value of the next element after the window

eg
maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 3);

[1, 2, 5, 2, 8, 1, 5]
 ^.....^              = 8

[1, 2, 5, 2, 8, 1, 5]
    ^.....^
 -1       +2          = 8 - 1 + 2 = 9

time complexity = O(n)
space complexity = O(1)


## divide and conquer

_dividing a data set into smaller chinks and then repeating a process with a subset of data_
- this can tremendously **decrease time complexity**

eg. given a sorted array of integers, write a function called search, that accepts a value and returns the index where the value passed to the function is located. if the value is not found, return -1

```js
search([1, 2, 3, 4, 5, 6], 4); // 3
search([1, 2, 3, 4, 5, 6], 6); // 5
search([1, 2, 3, 4, 5, 6], 11); // -1
```

shit solution:
```js
function search(arr, val) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === val) {
      return i;
    }
  }
  return -1;
}
```
this is called a linear search
- time complexity = O(n)

better solution:
```js
function search(arr, val) {
  let min = 0;
  let max = array.length - 1;

  while (min <= max) {
    let middle = Math.floor((min + max) / 2);
    let currentElement = array[middle];

    if (array[middle] < val) {
      min = middle + 1;
    } else if (array[middle] > val) {
      max = middle - 1;
    } else {
      return middle;
    }
  }

  return -1;
}
```
this is called a binary search
- time complexity = O(logn)


[>>> Next Page >>>](https://github.com/hungrypc/data-structures-and-algorithms/blob/master/chapters/5__optional_challenges.md)