# singly linked list

what is it?
it's a data structure that contains a **head, tail, and length** property. linked lists consists of nodes, and each **node** has a **value** and a **pointer** to another node or null
- there is no index so if you want to access a specific node, you start from the beginning and continually ask for the next node until you hit the node you were looking to access
- **singly linked** means that each node is only connected in one direction (the next node)

### comparisons with arrays

lists:
- do not have indexes
- connected via nodes with a **next** pointer
- random accesss is not allowed

arrays:
- indexed in order
- insertion and deletion can be expensive
- can quickly be accessed at a specific index

## coding our singly linked list

### starter code
```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}

let list = new SinglyLinkedList();

let first = new Node(1);
```

### push()
pseudocode:
- should accept a value
- create a new node using the value passed to the function
- if there is no head property on the list, set the head and the tail to be the newly created node
- otherwise set the next property on the tail to be the new node and set the tail property on the list to be the newly crated node
- increment the length by one
- return the linked list
```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  push(val) {
    let node = new Node(val);
    if (!this.head) {
      this.head = node;
      this.tail = this.head;
    } else {
      this.tail.next = node;
      this.tail = node;
    }
    this.length++;
    return this;
  }
}
```

### pop()
psuedocode :
- if there are no nodes in the list, return undefined
- loop through the list until you reach the tail
- set the next property of the second to last node to be null
- set the tail to be the second to last node
- decrement the length of the list by 1
- return the value of the node removed
```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  pop() {
    if (!this.head) {
      return undefined;
    } else {
      let current = this.head;
      let pre = current;
      while (current.next) {
        pre = current;
        current = current.next;
      }
      this.tail = pre;
      this.length--;
      if (this.length === 0) {
        this.head = null;
        this.tail = null;
      }
      return current;
    }
  }
}
```

HOWEVER, this version of pop isn't as clean as it can be, we'll refactor this later with a function that we'll write below

### shift()
psudeocode :
- if there are no nodes, return undefined
- store the current head property in a variable
- set the head property to be the curernt head's next property
- decrement the length by 1
- return the value of the node removed
```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  shift() {
    if (!this.head) {
      return undefined;
    } else {
      let current = this.head;
      this.head = current.next;
      this.length--;
      if (this.length === 0) {
        this.tail = null;
      }
      return current;
    }
  }
}
```

### unshift()
psuedocode :
- this function should accept a value
- create a new node using the value passed to the function
if there is no head property on the list, set the head and tail to be the newly created node
- otherwise set the newly created node's next property to be the current head property on the list
- set the head property on the list to be that newly created node
- increment the length of the list by 1
- return the linked list
```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
  unshift(val) {
    let newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head = newNode;
      this.length++;
      return this;
    }
  }
}
```


















