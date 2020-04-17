# binary search trees

binary trees
- each node can have at most 2 children

binary search trees
- same as binary tree except they are sorted/organized in a particular way
- used to store data that can be compared
  - every node to left of parent is **always less** than the parent
  - every node to right of parent is **always greater** than the parent

### starter code
```js
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }
}
```

### insert()
can be done interatively or recursively
psuedocode:
- create a new node
- starting at the root
  - check if there is a root, if not - root = new node
  - if there is a root, check if the value of the new node is greater or less than the value of the root
  - if it is greater
    - check to see if there is a node to the right
      - if there is, move to that node and repeat these steps
      - if there is not, add that node as the right property
  - if it is less
    - check to see if there is a node to the left
      - if there is, move to that node and repeat these steps
      - if there is not, add that node as the left property




























