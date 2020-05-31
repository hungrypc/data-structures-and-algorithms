# stacks and queues

## stacks
a **LIFO** data structure
  - **L**ast **I**n **F**irst **O**ut
  - the last element added to the stack will be the first element removed from the stack

how is it used?
- like a stack of plates, as you pile it up, the last thing (or the topmost plate) is what gets removed first.

where are stacks used?
- managing function invocations
- undo/redo
- routing (the history object) is treated like a stack

### creating a stack with an array
either push() and pop()
OR
shift() and unshift()

as long as we're removing from the same direction.
- though it's better to push and pop because they don't require reindexing

## writing our own stack from scratch
writing our push and pop methods for stacks are similar to how we wrote them in our linked lists, BUT stacks require that these methods be O(1) time.

### starter code
```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}
```

### push()
psuedocode:
- the function should accept a value
- create a new node with that value
- if there are no nodes in the stack, set the first and last peroperty to be the newly created node
- otherwise, create a variable that stores the current first property on the stack
- reset the first property to be the newly created node
- set the next property on the node to be the previously created variable
- increment the size of the stack by 1
```js
class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  push(val) {
    let newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      let temp = this.first;
      this.first = newNode;
      newNode.next = temp;
    }
    return ++this.size;
  }
}
```

### pop()
psuedocode:
- if there are no nodes in the stack, return null
- create a temporary variable to store the first property on the stack
- if there is only 1 node, set the first and last property to be null
- otherwise, set the first property to be the next property on the current first
- decrement the size by 1
-  return the value of the node removed
```js
class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  pop(val) {
    let newNode = new Node(val);
    if (!this.first) return null;
    let temp = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = temp.next;
    this.size--;
    return temp.value;
  }
}
```

### big O
methods     | big o
------------|--------
insertion   | O(1)
removal     | O(1)
searching   | O(n)
access      | O(n)

## final form:
```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  push(val) {
    let newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      let temp = this.first;
      this.first = newNode;
      newNode.next = temp;
    }
    return ++this.size;
  }

  pop(val) {
    let newNode = new Node(val);
    if (!this.first) return null;
    let temp = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = temp.next;
    this.size--;
    return temp.value;
  }
}
```

## queues
a **FIFO** data structure
- **F**irst **I**n **F**irst **O**ut
- first element added will be the first element removed

how is it used?
- background tasks
- uploading resources
- printing / task processing

why?
- queues are useful for processing tasks and are foundational for more complex data structures

## writing our own stack from scratch

### starter code
```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}
```

### enqueue()
psuedocode:
- this function accepts some value
- create a new node using the value passed
- if there are no nodes in the queue, set this node to be the first and last property of the queue
- otherwise, set the next property on the current last to be that node, and then set the last proerty of the queue to be that node
- increment size of queue by 1
- return
```js
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  enqueue(val) {
    let newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    return ++this.size;
  }
}
```

### dequeue()
psuedocode:
- if there is no first property, return null
- store the first property in a variable
- if there is only 1 node, set the first and last to be null;
- if there is more than 1 node, set the first property to be the next property of first
- decrement the size by 1
- return the value of the node dequeued
```js
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  dequeue() {
    if (!this.first) return null;
    let temp = this.first;
    if (this.size === 1) {
      this.last = null;
    }
    this.first = temp.next;
    this.size--;
    return temp.value;
  }
}
```

### big O

method    | big O
----------|--------
insertion | O(1)
removal   | O(1)
searching | O(n)
access    | O(n)

## final form:
```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  enqueue(val) {
    let newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    return ++this.size;
  }

  dequeue() {
    if (!this.first) return null;
    let temp = this.first;
    if (this.size === 1) {
      this.last = null;
    }
    this.first = temp.next;
    this.size--;
    return temp.value;
  }
}
```

