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
      this.tail = this.head;
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }
}
```

### get()
psuedocode :
- this function should accept an index
- if the index is less than zero or greater than/equal to the length of the list, return null
- loop thought the list until you reach the index and return the node at that specific index
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
  get(index) {
    if (index < 0 || index >= this.length) {
      return null;
    } else {
      let count = 0;
      let current = this.head;
      while (count !== index) {
        current = current.next;
        count++;
      }
      return current;
    }
  }
}
```

### set()
psuedocode :
- this function should accept an index and a value
- use your **get()** function to find the specific node
- if the node is not found, return false
- if the node _is_ found, set the value of that node to be the value passed to the function and return true
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
  set(index, val) {
    let node = this.get(index);
    if (node) {
      node.val = val;
      return true;
    }
    return false;
  }
}
```

### insert()
psuedocode :
- if the index is less than zero / greater than the length, return false
- if the index is the same as the length, push a new node to the end of the list
- if the index is 0, unshift a new node to the start of the list
- otherwise, using th **get** method, access the node at the index - 1
- set the next property on that node to be the new node
- set the next property on the new node to be the previous next
- increment the length
- return true
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
  insert(index, val) {
    if (index < 0 || index > this.length) {
      return false;
    } else if (index === this.length) {
      return !!this.push(val);
    } else if (index === 0) {
      return !!this.unshift(val);
    } else {
      let newNode = new Node(val);
      let pre = this.get(index - 1);
      let temp = pre.next;
      pre.next = newNode;
      newNode.next = temp;
      this.length++;
      return true;
    }
  }
}
```

### remove()
psuedocode :
- if the index is less than zero or greater than the length, return undefined
- if the index is the same as the length - 1, pop
- if the index is 0, shift
- otherwise, using the **get** method, access the node at the index -1
- set the next property on that node to be the next of the next node
- decrement the length
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
  remove(index) {
    if (index < 0 || index > this.length) {
      return undefined;
    } else if (index === this.length - 1) {
      return this.pop();
    } else if (index === 0) {
      return this.unshift();
    } else {
      let pre = this.get(index - 1);
      let removed = pre.next;
      pre.next = removed.next;
      this.length--;
      return removed;
    }
  }
}
```

### reverse()
psuedocode :
- swap the head and the tail
- create a variable called next
- create a variable called prev
- create a variable called node and initialize it to the head property
- loop through the list
- set the next to be the next property on whatever node is
- set the next property of the node to be whatever prev is
- set prev to be the value of the node variable
- set the node variable to be the value of the next variable
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
  reverse() {
    let next = null;
    let prev = null;
    let node = this.head;
    this.head = this.tail;
    this.tail = node;
    for (let i = 0; i < this.length; i++) {
      next = node.next;
      node.next = prev;
      prev = node;
      node = next;
    }
    return this;
  }
}
```


## big O of singly linked lists

method    | time complexity
----------|----------------
insertion | O(1)
removal   | O(1) or O(n)
searching | O(n)
access    | O(n)

### recap
- singly linked lists are an excellent alternative to arrays when insertion and deletion at the beginning are frequently required
- arrays contain a built in index whereas linked lists do not
- the idea of a list data structure that consists of nodes is the foundation for other data structures like stacks and queues



## final form:
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

  unshift(val) {
    let newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = this.head;
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }

  get(index) {
    if (index < 0 || index >= this.length) {
      return null;
    } else {
      let count = 0;
      let current = this.head;
      while (count !== index) {
        current = current.next;
        count++;
      }
      return current;
    }
  }

  set(index, val) {
    let node = this.get(index);
    if (node) {
      node.val = val;
      return true;
    }
    return false;
  }

  insert(index, val) {
    if (index < 0 || index > this.length) {
      return false;
    } else if (index === this.length) {
      return !!this.push(val);
    } else if (index === 0) {
      return !!this.unshift(val);
    } else {
      let newNode = new Node(val);
      let pre = this.get(index - 1);
      let temp = pre.next;
      pre.next = newNode;
      newNode.next = temp;
      this.length++;
      return true;
    }
  }

  remove(index) {
    if (index < 0 || index > this.length) {
      return undefined;
    } else if (index === this.length - 1) {
      return this.pop();
    } else if (index === 0) {
      return this.unshift();
    } else {
      let pre = this.get(index - 1);
      let removed = pre.next;
      pre.next = removed.next;
      this.length--;
      return removed;
    }
  }

  reverse() {
    let next = null;
    let prev = null;
    let node = this.head;
    this.head = this.tail;
    this.tail = node;
    for (let i = 0; i < this.length; i++) {
      next = node.next;
      node.next = prev;
      prev = node;
      node = next;
    }
    return this;
  }
}
```

























