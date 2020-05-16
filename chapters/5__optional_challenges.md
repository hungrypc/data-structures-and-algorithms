# optional challenges

## frequency counter

write a function called sameFrequency. given two positive integers, find out if the two numbers have the same frequency of digits.
your solution **must** have a time complexity of O(n)

```js
sameFrequency(182, 281); // true
sameFrequency(34, 14); // false
sameFrequency(22, 222); // false
```
```js
function sameFrequency(n1, n2) {
  let str1 = n1.toString();
  let str2 = n2.toString();
  let map = {};
  if (str1.length !== str2.length) {
    return false;
  }
  for (const digit of str1) {
    map[digit] ? map[digit] += 1 : map[digit] = 1;
  }
  for (const digit of str2) {
    if (map[digit]) {
      map[digit] -= 1;
    } else {
      return false;
    }
  }
  return true;
}
```


## frequency counter / multiple pointers

write a function called areThereDuplicates which accepts a variable number of arguments, and checks whether there are any duplicates among the arguments passed in.

restrictions:
- time = O(n)
- space = O(n)

```js
areThereDuplicates(1, 2, 3); // false
areThereDuplicates(1, 2, 2); // true
areThereDuplicates('b', 'a', 'c', 'a'); // true
```
```js
function areThereDuplicates() {
  let map = {};
  for (let i = 0; i < arguments.length; i++) {
    let value = arguments[i];
    if (map[value]) {
      return true;
    } else {
      map[value] = 1;
    }
  }
  return false;
}
```


## multiple pointers

write a function called averagePair. given a sorted array of integers and a target average, determine if there is a pair of values in the array where the average of the pair equals the target average. there may be more than one pair that matches the average target

constraints:
- time = O(n)
- space = O(1)

```js
averagePair([1, 2, 3], 2.5); // true
averagePair([1, 3, 3, 5, 6, 7, 10, 12, 19], 8); // true
averagePair([-1, 0, 3, 4, 5, 6], 4.1); // false
averagePair([], 4); // false
```
```js
function averagePair(arr, target) {
  let left = 0;
  let right = left + 1;
  while (left < arr.length - 1) {
    let avg = (arr[left] + arr[right]) / 2;
    if (avg === target) return true;
    if (right === arr.length - 1) {
      left += 1;
      right = left + 1;
    } else {
      right += 1;
    }
  }
  return false;
}

```


## multiple pointers

write a function called isSubsequence which takes in two strings and checks whether the characters in the first string form a subsequence of the characters in the second string. in other words, the function should check whether the characters in the first string appear somewhere in the second string, without their order changing.

constraints:
- time = O(n + m)
- space = O(1)

```js
isSubsequence('hello', 'hello world'); //true
isSubsequence('sing', 'sting'); // true
isSubsequence('abc', 'abracadabra'); // true
isSubsequence('abc', 'acb'); // false
```
```js
function isSubsequence(str1, str2) {
  let i = 0;
  let j = 0;
  if (!str1) return true;
  while (j < str2.length) {
    if (str1[i] === str2[j]) i++;
    if (i === str1.length) return true;
    j++;
  }
  return false;
}

```

## sliding window

given an array of integers and a number, write a function called maxSubarraySum which find the maximum sum of a subarray with the length of the number passed to the function

note that the subarray must consist of consecutive elements from the original array.

constraints:
- time = O(n)
- space = O(1)

```js
maxSubarraySum([100, 200, 300, 400], 2); // 700
maxSubarraySum([1, 4, 2, 10, 23, 3, 1, 0, 20], 4); // 39
maxSubarraySum([-3, 4, 0, -2, 6, -1], 2); // 5
maxSubarraySum([3, -2, 7, -4, 1, -1, 4, -2, 1], 2); // 5
maxSubarraySum([2, 3], 3); // null
```
```js
function maxSubarraySum(arr, target) {
  let maxSum = 0;
  let temp = 0;
  if (arr.length < target) return null;
  for (let i = 0; i < target; i++) {
    maxSum += arr[i];
  }
  temp = maxSum;
  for (let i = target; i < arr.length; i++) {
    temp = temp - arr[i - target] + arr[i];
    maxSum = Math.max(maxSum, temp);
  }
  return maxSum;
}

```

## sliding window

Write a function called minSubArrayLen which accepts two parameters - an array of positive integers and a positive integer

This function should return the minimal length of a contiguous subarray of which the sum is greater than or equal to the integer passed to the function. If there isn't one, return 0 instead.

constraints:
- time = O(n)
- space = O(1)

```js
minSubArrayLen([2, 3, 1, 2, 4, 3], 7); // 2 ([4, 3])
minSubArrayLen([2, 1, 6, 5, 4], 9); // 2
minSubArrayLen([3, 1, 7, 11, 2, 9, 8, 21, 62, 33, 19], 52); // 1 ([62])
```
```js
function minSubArrayLen(nums, s) {
  if (!nums.length) return 0;

  let min = Infinity;
  let left = 0;
  let sum = 0;
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] >= s) return 1;
    sum += nums[i];
    while(sum >= s) {
      min = Math.min(min, i + 1 - left);
      sum -= nums[left]
      left++
    }
  }

  if (min === Infinity) return 0;
  return min;
}

```

## sliding window

Write a function called findLongestSubstring, which accepts a string and returns the length of the longest substring with all distinct characters

constraints:
- time = O(n)


```js
findLongestSubstring(""); // 0
findLongestSubstring("thisisawesome"); // 6
findLongestSubstring("bbbbbbb"); // 1
```
```js
function findLongestSubstring(string) {
  if (string.length === 0) return 0;

  let count = 0;

}

```

[>>> Next Page >>>](https://github.com/hungrypc/data-structures-and-algorithms/blob/master/chapters/6__recursion.md)


































