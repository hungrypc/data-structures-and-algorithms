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
```js
class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  insert(value) {
    let newNode = new Node(value);
    if (!this.root) {
      this.root = newNode;
      return this;
    } else {
      let current = this.root;
      while (true) {
        if (value === current.value) return undefined;
        if (value < current.value) {
          if (!current.left) {
            current.left = newNode;
            return this;
          }
          current = current.left;
        } else {
          if (!current.right) {
            current.right = newNode;
            return this;
          }
          current = current.right;
        }
      }
    }
  }
}
```

### find() / contains()
can be done interatively or recursively
psuedocode:
- starting at root
  - check if there's a root, if not - we're done searching
  - there there is a root, check if the value of the new node is the value we are looking for.
    - if found, we're done
    - if not, check to see if the value is greater than or less than the value of the root
      - if it is greater
        - check to see if there is a node to the right
          - if there is, move to that node and repeat these steps
          - if there is not, we're done searching
      - if it is less
        - check to see if there is a node to the left
          - if there is, move to that node and repeat these steps
          - if there is not, we're done searching
```js
class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  contains(value) {
    if (!this.root) return false;
    let current = this.root;
    let found = false;
    while(current && !found) {
      if (value < current.value) {
        current = current.left;
      } else if (value > current.value) {
        current = current.right;
      } else {
        return true;
      }
    }
    return false;
  }
}
```

### big O
method    | big O
----------|-------
insertion | O(log n)
searching | O(log n)

in general, its O(log n) BUT its NOT guaranteed though - there are some BST configs that are very slow

## final form:
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

  insert(value) {
    let newNode = new Node(value);
    if (!this.root) {
      this.root = newNode;
      return this;
    } else {
      let current = this.root;
      while (true) {
        if (value === current.value) return undefined;
        if (value < current.value) {
          if (!current.left) {
            current.left = newNode;
            return this;
          }
          current = current.left;
        } else {
          if (!current.right) {
            current.right = newNode;
            return this;
          }
          current = current.right;
        }
      }
    }
  }

  contains(value) {
    if (!this.root) return false;
    let current = this.root;
    let found = false;
    while(current && !found) {
      if (value < current.value) {
        current = current.left;
      } else if (value > current.value) {
        current = current.right;
      } else {
        return true;
      }
    }
    return false;
  }
}
```

























