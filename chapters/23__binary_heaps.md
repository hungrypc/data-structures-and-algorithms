# binary heaps

what is a binary heap?
- **very** similar to a BST, but with some different rules
  - like BST, can only have at most 2 children
  - BUT, there is no order rules for left and right, only...
- **MaxBinaryHeap**
  - parent nodes are always larger than child nodes
- **MinBinaryHeap**
  - parent nodes are always smaller than child nodes
- but, there are no guarantees between sibling nodes
- binary heaps are as compact as possible, all the children (left and right) of each node are as full as they can be and left children are filled out first

binary heaps are used to implement *priority queues*, which are very commonly used data structures.
they're also used quite a bit with **graph traversal** algorithms


## storing heaps
we can actually use an array to represent a binary heap
- for any **index** of an array **n**
  - the left child is stored at **2n + 1**
  - the right child is stored at **2n + 2**

what if we have a child node and want to find its parent?
- for any child node at index n
  - its parent is at index Math.floor((n - 1) / 2)

## writing our binary heaps

### insert
push to end of the list, then bubble up the value to get it to its correct position
- we bubble it up by comparing the value to its parent

psuedocode:
- push the value into the values property on the heap
- bubble the value up to its correct spot
  - create a variable called index which is the length of the values property -1
  - create a variable called parentIndex which is the floor of (index - 1) / 2
  - keep looping as long as the values element at the parentIndexis less than the values element at the child index
    - swap the value of the values element at the parentIndex with the value of the element property at the child index
    - set the index to be the parentIndex, and start over







































