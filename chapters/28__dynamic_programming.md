# Dynamic Programming

## What is Dynamic Programming?
_A method for solving a complex problem by breaking it down into a collection of simpler subproblems, solving each of those subproblems just once, and storing their solutions._

However, this will only work on problems with:
1. An optimal substructure
2. Overlapping subproblems

### Overlapping Subproblems
> A problem is said to have **overlapping subproblems** if it can be broken down into subproblems which are reused several times.

For example, the fibonacci sequence:
```
Every number after the first two is the sum of the two preceding ones
1 1 2 3 5 8 13 21 34 ...
```

Any time we're trying to derive some digit (say, the 5th number in the sequence), we break it down into a smaller piece
- take the 4th digit and add it to the 3rd
- but to find the 4th, we have to add the 3rd and the 2nd
- and to find the 3rd, we have to add the 2nd and the 1st

So there are subproblems here, we break down one problem into smaller steps.

This is often done in recursion - when we write recursive solutions, there are subproblems involved.\
**! but that doesn't mean that they overlap !**\
For overlapping subproblems, we need to look for repetition - if we are repeating the subproblem(s).

### Optimal Substructure
> A problem is said to have **optimal substructure** if an optimal solution can be constructed from optimal solutions of its subproblems.

For example, finding the shortest path:
```
Find the shortest path from A to D
A - 2 -> B
B - 3 -> C
B - 2 -> E
E - 2 -> C
C - 1 -> D
```
This has optimal substructure because we can construct the optimal solution from A to D from the subproblems and *their* optimal solutions
- A to D: A -> B -> C -> D
- A to C: A -> B -> C
- A to B: A -> B

## Breaking It Down
Let's take a problem that exhibits the two features we just explored and solve it, first without dynamic programming, and then refactor the solution to include dynamic programming.

### The Fibonacci Sequence:
Here's what we know:
- to get the the 5th fibonacci number, we add the 4th fibonacci number and the 3rd fibonacci number
  - fib(5) = fib(4) + fib(3)
  - fib(n) = fib(n - 1) + fib(n - 2)
- fib(2) = 1
- fib(1) = 1
```js
// recursive solution
function fib(n) {
  if (n <= 2) return 1;
  return fib(n - 1) + fib(n - 2);
}
```
HOWEVER, this is **not** a great solution.\
As n grows, the number of operations increase **A LOT**\
In terms of big O, it's' O(2^n) (even worse than O(n^2)).

The problem is that we are repeating things.
- fib(5) = fib(4) + fib(3)
- but to calculate fib(4) we calculate fib(3)
- with recursion, we're actually doing the calculation for fib(3) **twice**
- imagine how many repetition is going on as n increases

**This is where Dynamic Programming comes in.**
> Using past knowledge to make solving future problems easier

### Memoization
*Storing the results of expensive function calls and returning the cached result when the same inputs occur again.*
```js
//  memoized solution
function fib(n, memo = []) {
  if (memo[n] !== undefined) return memo[n];
  if (n <= 2) return 1;
  let res = fib(n - 1, memo) + fib(n - 2, memo);
  memo[n] = res;
  return res;
}
```
This is **much** faster, with a time complexity of O(n).

### Tabulation
So far, everything we've been doing has been a **top-down** approach. We start from the top (what we're trying to find) and keep going down to fill in the gaps until we hit our base case (where we add everything together).

HOWEVER, we can use another approach: **bottom-up**. This can be done via Tabulation:\
*Storing the result of a previous result in a "table" (usually an array).*

This is usually done using iteration. Better **space complexity** can be achieved using tabulation.
```js
//  tabulated solution
function fib(n) {
  if (n <= 2) return 1;
  let fibNums = [0, 1, 1]
  for (let i = 3; i <= n; i++) {
    fibNums[i] = fibNums[i - 1] + fibNums[i - 2];
  }
  return fibNums[n];
}
```

So, because the memoized version still uses recursion, we run the risk of reaching the maximum stack at really large numbers (takes up a lot of space). The tabulated version wouldn't run into this problem because it doesn't take anywhere near as much space.
