# Dynamic Programming

## What is Dynamic Programming?
_A method for solving a complex problem by breaking it down into a collection of simpler subproblems, solving each of those subproblems just once, and storing their solutions._

However, this will only work on problems with:
1. An optimal substructure
2. Overlapping subproblems

### Overlapping Subproblems
A problem is said to have **overlapping subproblems** if it can be broken down into subproblems which are reused several times.

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































