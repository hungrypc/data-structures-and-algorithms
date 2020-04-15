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

write a function called averagePair. given a sorted array of integers and a target average, determine if there is a pair of values in the arary where the average of the pair equals the target average. there may be more than one pair that matches the average target

constraints:
- time = O(n)
- space = O(1)

```js
averagePair([1, 2, 3], 2.5); // true
averagePair([1, 3, 3, 5, 6, 7, 10, 12, 19], 8); // true
averagePair([-1, 0, 3, 4, 5, 6], 4.1); // false
averagePair([], 4); // false
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


## sliding window

given an array of integers and a number, write a function called maxSubarraySum which find the maximum sum of a subarray with the length of the number passed to the function

note that the subarra must consist of consecutive elements from the original array.

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






































