# analyzing performance of arrays and objects

## objects

when to use them:
- when you don't need order
- when you need fast access / insertion and removal

bigO of objects:
- insertion: O(1)
- removal: O(1)
- searching: O(n)
  - not searching by key, searching values for a certain condition
- access: O(1)

bigO of object methods:

method         | bigO
-------------- | ------
Object.keys    | O(n)
Object.values  | O(n)
Object.entries | O(n)
hasOwnProperty | O(1)


## arrays

when to use arrays:
- when you need order
- when you need fast access / insertion and removal (sort of...)

bigO of arrays:
- insertion: it depends...
  - push is alright, but unshift means re-indexing
- removal: it depends...
  - pop is alright, but shift means re-indexing
- access: O(1)
- searching: O(n)

bigO of array methods:

method  | bigO
------- | ------
push    | O(1)
pop     | O(1)
shift   | O(n)
unshift | O(n)
concat  | O(n)
slice   | O(n)
splice  | O(n)
sort    | O(n logn)
etc     | O(n)

note: etc = forEach/map/filter/reduce/etc


[C3 - Problem Solving Approach](https://github.com/hungrypc/data-structures-and-algorithms/blob/master/chapters/3__problem_solving_approach.md)
