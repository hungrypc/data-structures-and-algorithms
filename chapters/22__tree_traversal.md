# tree traversal

the main objective of tree traversal: **how do we visit every node ONCE**

## breadth-first search
where we visit every node on the same level (sibling nodes) *before* visting children nodes
- working horizontally

### writing our BFS
psuedocode:
- create a queue (this can be an array) and a variable to store the values of nodes visited
- place the root node in the queue
- loop as long as there is anything in the queue
  - dequeue a node from the queue and push the value of the node into the variable that stores the nodes
  - if there is a left property on the node dequeued - add it to the queue
  - if there is a right property on the node dequeued - add it to the queue
- return the variable that stores the values
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

  BFS() {
    let node = this.root;
    let data = [];
    let queue = [];
    queue.push(node);
    while(queue.length) {
      node = queue.shift();
      data.push(node);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    return data;
  }
}
```

## depth-first search
where we visit nodes vertically, down to the end of the tree, before visiting sibling nodes

### preOrder (n l r)
- visit **self (node) first**
- visit left next all the way down
- visit right

psuedocode:
- create a variable to store the values of nodes visited
- store the root of the BST in a variable called current
- write a helper function which accepts a node
  - push the value of the node to the variable that stores the values
  - if the node has a left property, call the helper function with the left property on the node
  - if the node has a right property, call the helper function with the right property on the node
- invoke the helper function with the current variable
- return the array of values of node visited
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

  DFSPreOrder() {
    let current = this.root;
    let data = [];
    function traverse(node) {
      data.push(node.val);
      if (node.left) traverse(node.left);
      if (node.right) traverse(node.right);
    }
    traverse(current);

    return data;
  }
}
```

### postOrder (l r n)
- visit **left first** all the way down until there is no left side
- once there are no more lefts to visit, hit right
- if there are no rights, visit self (node)

psuedocode:
create a variable to store the values of nodes visited
- store the root of the BST in a variable called current
- write a helper function which accepts a node
  - if the node has a left property, call the helper function with the left property on the node
  - if the node has a right property, call the helper function with the right property on the node
  - push the value of the node to the variable that stores the values
  - invoke the helper function with the current variable
- return the array of values
```js
class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  DFSPostOrder() {
    let current = this.root;
    let data = [];
    function traverse(node) {
      if (node.left) traverse(node.left);
      if (node.right) traverse(node.right);
      data.push(node.val);
    }
    traverse(current);

    return data;
  }
}
```

### inOrder (l n r)
- visit left all the way down
- visit self (node)
- visit right

psuedocode:
- create a variable to store the values of nodes visited
- store the root of the BST in a variable called current
- write a helper function which accepts a node
  - if the node has a left property, call the helper function with the left property on the node
  - push the value of the node to the variable that stores the values
  - if the node has a right property, call the helper function with the right property on the node
- invoke the helper function with the current variable
- return the array of values
```js
class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  DFSInOrder() {
    let current = this.root;
    let data = [];
    function traverse(node) {
      if (node.left) traverse(node.left);
      // node.left && traverse(node.left); // this does the same
      data.push(node.val);
      if (node.right) traverse(node.right);
      // node.right && traverse(node.right); // this does the same
    }
    traverse(current);

    return data;
  }
}
```

## when to use BFS and DFS

depends on the tree.
- in a tree thats wide and tall
  - BFS takes up more memory -> gotta visit many many nodes to reach bottom (queue stacks up)
  - DFS uses less memory -> hits bottom with less nodes
- in a tree that's one sided and linear
  - BFS takes up less memory -> only ever one node in the queue per node visited
  - DFS takes up more memory -> queue stacks up

(most trees look like the first tree described)

## when to use preOrder/postOrder/inOrder

- inOrder actually returns the values of the nodes in ascending order (for BST)
- preOrder can be useful if you're trying to clone/duplicate/export a tree structure so that it is easily reconstructed or copied
- postOrder (?)
