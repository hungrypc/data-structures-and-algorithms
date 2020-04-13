# big O notation

## intro

eg: write a function that calculates the sum of all numbers from 1 up to (and including) n

solution 1:
```js
function addUpTo(n) {
  let total = 0;
  for (let i = 1; i <= n; i++) {
    total += 1;
  }
  return total;
};
```

solution 2:
```js
function addUpTo(n) {
  return n * (n + 1) / 2;
};
```

which is better, solution 1 or solution 2?

**big O allows us to assign a value in general terms to talk about how code compares to other code without having to actually time each function**

let's count the number of simple operations the computer has to perform

solution 2 has three operations happening:
  1. multiplication (n *)
  2. addition (n + 1)
  3. division ( / 2)

solution 1 has n operations happening because it's in a loop.
  - n additions (total += 1; i++)
  - n assignments (total += 1; i++)
  - 2 assignment (i = 1; total = 0)
  - n comparisons (i <= n)
depending on what we count, number of opeations can be as low as 2n or as high as 5n. regardless of the exact number, the number of operations grows roughly proportionally with n

SO...

for solution 1
  - as n increases, time increases (linearly)
  - this is bounded by n; bigO = O(n)

for solution 2
  - as n grows, the time doesn't really change - there's always 3 operations that happen
  - this is constant; bigO = O(1)

**big O helps us describe the relationship b/t input size and time relative to that input**

eg 2:
```js
function printAllPairs(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
}
```
this shows an O(n) operations *inside* of an O(n) operation = **O(n^2)**
  - plotted on a graph: as n grows, time grows exponentially (quadratic)


## simplifying bigO expressions

some rules for simplyfying:
1. constants don't matter
  - O(2n) = O(n)
  - O(500) = O(1)
  - O(13n^2) = O(n^2)
2. smaller terms don't matter
  - O(n + 10) = O(n)
  - O(1000n + 50) = O(n)
  - O(n^2 + 5n + 8) = O(n^2)

bigO shorthands:
1. arithmetic operations are constant
2. variable assignment is constant
3. accessing elements in an array (by index) or object (by key) is constant
4. in a loop, the complexity = the length of the loop * the complexity of whatever happens inside the loop

more examples:
```js
function logAtLeastFive(n) {
  for (let i = 1; i <= Math.max(5, n); i++) {
    console.log(i);
  }
}
```
this function logs up to n, unless n <= 5 where the function will log up to 5 regardless.

as n grows, it takes longer to log up to n = O(n)

```js
function logAtMostFive(n) {
  for (let i = 1; i <= Math.min(5, n); i++) {
    console.log(i);
  }
}
```
this function does the opposite, where if n >= 5 it will log only up to 5

as n grows, it only logs up to 5 = O(1)


## space complexity

so far, we're only been talking about **time complexity**.
let's talk about what happens to the space that an algorithm takes up as n increases

we can still use big O notation to represent this.

**auxiliary space** refers to space required by the algorithm, not including space taken up by the inputs
(we're going to ignore fact that space grows as input size grows because that's already obvious)

some rules of thumb:
1. most primitives (booleans, numbers, undefined, null) are constant space
2. strings require O(n) space (where n in the string length)
3. reference types are generally O(n), where n is the length (for arrays) or the number of keys (for objects)

example:
```js
function sum(arr) {
  let total = 0;
  for (let i = 0; i < arr.length; i++) {
    total += arr[i];
  }
  return total;
}
```
for this example, no matter the size of the input, the function only needs space for two things:
1. total
2. i

this means there is constant space = O(1) space

another example:
```js
function double(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    newArr.push(2 * arr[i]);
  }
  return newArr;
}
```
as the input grows, our newArr gets longer as well (newArr.push(...))
this means that the space is bound by n = O(n) space


## logarithms

whats a log again? its the inverse of expenentiation

log2(8) = 3   ->    2^3 = 8
log2(value) = exponent    ->    2^exponent = value

we'll omit the 2 for bigO (log === log2)
essentially: _the logarithm of a number roughly measures the number of times you can divide that number by 2 **before you get a value that's less than or equal to one**_

O(log n) time complexity is really good
O(nlog n) isnt great (it's worse than O(n) but its better than O(n^2))


[bigO cheatsheet](https://www.bigocheatsheet.com/)

