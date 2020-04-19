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
  - keep looping as long as the values element at the parentIndex is less than the values element at the child index
    - swap the value of the values element at the parentIndex with the value of the element property at the child index
    - set the index to be the parentIndex, and start over

```js
class MaxBinaryHeap {
  constructor() {
    this.values = [];
  }

  insert(element) {
    this.values.push(element);
    this.bubbleUp();
  }

  bubbleUp() {
    let index = this.values.length - 1;
    const element = this.values[index];
    while (index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      let parent = this.values[parentIndex];
      if (element <= parent) break;
      this.values[parentIndex] = element;
      this.values[index] = parent;
      index = parentIndex;
    }
  }
}
```

### extractMax
the procedure for deleting the root from the heap (effectively extracting the maximum element in a max-heap or the minimum element in a min-heap) and restoring the properties is called *trickle-down/bubble-down/etc*
- remove the root
- replace root with the most recently added
- adjust (trickle-down)

psuedocode:
- swap the first value in the values property with the last one
- pop from the values property, so you can return the value at the end
- have the new root 'sink down' to the correct spot
  - your parent index starts at 0 (the root)
  - find the index of the left child: 2 * index + 1
    - make sure it's not out of bounds
  - find the index of the right child: 2 * index + 2
    - make sure it's not out of bounds
  - if the left or right child is greater than the element, swap
    - if both are larger, swap with the largest child
  - keep looping and swapping until neither child is larger than the element
  - return old root

```js
class MaxBinaryHeap {
  constructor() {
    this.values = [];
  }

  extractMax() {
    const max = this.values[0];
    const end = this.values.pop();
    if (this.values.length > 0) {
      this.values[0] = end;
      this.bubbleDown();
    }
    return max;
  }

  bubbleDown() {
    let index = 0;
    const length = this.values.length;
    const element = this.values[index];
    while (true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let leftChild, rightChild;
      let swap = null;

      if (leftChildIndex < length) {
        leftChild = this.values[leftChildIndex];
        if (leftChild > element) {
          swap = leftChildIndex;
        }
      }
      if (rightChildIndex < length) {
        rightChild = this.values[rightChildIndex];
        if (
          (!swap && rightChild > element) ||
          (!swap && rightChild > leftChild)
        ) {
          swap = rightChildIndex;
        }
      }

      if (!swap) break;
      this.values[index] = this.values[swap];
      this.values[swap] = element;
      index = swap;
    }
  }
}
```

### priority queue

a data structure where each element has a priority. elements with higher priorities are served before elements with lower priorities
- separate from heaps -> just a generic abstract concept that can be implemented in many ways (most commonly via heaps)
- lower number = higher priority

to implement priority queues, we can actually use heaps
- all that we care about is the top level element (min or max thing)
- every time we add something in, the heap will be updated (serve higher priority over lower priority)
- every time we removed something, we remove from the top (finish serving highest priority)

### starter code
```js
class Node {
  constructor(val) {
    this.val = val;
    this.priority = null;
  }
}
class PriorityQueue {
  constructor() {
    this.values = [];
  }
}
```
note: we're going to be implementing a MinBinaryHeap

psuedocode:
- write a Min Binary Heap = lower number means higher priority
- each node has a val and a priority. use the priority to build the heap
- **enqueue** method accepts a value and priority, makes a new node, and puts it in the right spot based off its priority
- **dequeue** method removes root element, returns it, and rearranges heap using priority
```js
class Node {
  constructor(val, priority) {
    this.val = val;
    this.priority = priority;
  }
}

class PriorityQueue {
  constructor() {
    this.values = [];
  }

  enqueue(val, priority) {
    let newNode = new Node(val, priority);
    this.values.push(newNode);
    this.bubbleUp();
  }

  bubbleUp() {
    let index = this.values.length - 1;
    const element = this.values[index];
    while (index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      let parent = this.values[parentIndex];
      if (element.priority >= parent.priority) break;
      this.values[parentIndex] = element;
      this.values[index] = parent;
      index = parentIndex;
    }
  }

  dequeue() {
    const min = this.values[0];
    const end = this.values.pop();
    if (this.values.length > 0) {
      this.values[0] = end;
      this.bubbleDown();
    }
    return min;
  }

  bubbleDown() {
    let index = 0;
    const length = this.values.length;
    const element = this.values[index];
    while (true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let leftChild, rightChild;
      let swap = null;    // keeps track of position we'll swap w/

      if (leftChildIndex < length) {   // checking out of bounds
        leftChild = this.values[leftChildIndex];
        if (leftChild.priority < element.priority) {
          swap = leftChildIndex;
        }
      }
      if (rightChildIndex < length) {   // checking out of bounds
        rightChild = this.values[rightChildIndex];
        if (
          (!swap && rightChild.priority < element.priority) ||
          (!swap && rightChild.priority < leftChild.priority)
        ) {
          swap = rightChildIndex;
        }
      }

      if (!swap) break;
      this.values[index] = this.values[swap];
      this.values[swap] = element;
      index = swap;
    }
  }
}
```

however, the way we've written this doesn't really account for multiple nodes with the same priority, there's no guaranteed order between siblings
- we could add a time/resource property to each node so when comparing nodes with the same priority, we prioritize the one that came first/the one that uses least or most resources etc

## big O

binary heaps excel at insertion and removal

method    | big O
----------|-------
insertion | O(log n)
removal   | O(log n)
search    | O(n)

why is it log n?
- worst case, we insert something that needs to be put at root
  - we only need to compare per row of the heap
  - eg
    - for 16 elements, we only need 4 comparisons
    - for 32 elements, we only need 5 comparisons
  - every time we double the number of nodes, every new full new complete layer, we only increasing the time that it takes by 1
- binary heaps are not really made to be searchable
  - if you want to optimize search, probably want to use a binary search tree

