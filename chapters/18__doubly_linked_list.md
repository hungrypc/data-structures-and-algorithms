# doubly linked lists

almost identical to a singly linked list, except every node has **another** pointer, to the **previous** node

this allows for more flexibility, but the trade off is that it also takes up more memory

### starter code
```js
class Node {
  constructor(val) {
  this.val = vall;
  this.next = null;
  this.prev = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}
```

### push()
psuedocode:
- create a new node with the value passed to the function
- if the head property is null, set the head and tail to be the newly created node
- otherwise, set the next property on the tail to be that node
- set the previous property on the newly created node to be the tail
- set the tail to be the newly created node
- increment the length
- return the doubly linked list
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(val) {
    let newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }
}
```

### pop()
psuedocode:
- if there is no head, return undefined
- store the current tail in a variable to return later
- if the length is 1, set the head and the tail to be null
- update the tail to be the previous node
- set the newTail's next property to null
- decrement the length
- return the value removed
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  pop() {
    if (!this.head) return undefined;
    let poppedNode = this.tail;
    if(this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.tail = poppedNode.prev;
      this.tail.next = null;
      poppedNode.prev = null;
    }
    this.length--;
    return poppedNode;
  }
}
```

### shift()
psuedocode:
- if length is 0, return undefined
- store the curent head property in a variable
- if length = 1
  - set the head to null
  - set the tail to null
- update the head to be the next of the old head
- set the head's prev property to null
- set the old head's next property to null
- decrement the length
- return old head
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  shift() {
    if (this.length === 0) return undefined;
    let oldHead = this.head;
    if (length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.head = oldHead.next;
      this.head.prev = null;
      oldHead.next = null;
    }
    this.length--;
    return oldHead;
  }
}
```

### unshift()
psuedocode:
- create a new node with the value passed to the function
- if the length = 0
  - set the head to be the new node
  - set the tail to be the new node
- otherwise
  - set the prev property on the head to be the new node
  - set the next property on the new node to be the head
  - update the head of the list to be the new node
- increment the length
- return the list
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  unshift(val) {
    let newNode = new Node(val);
    if (this.length === 0) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.head.prev = newNode;
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }
}
```

### get()
psuedocode:
- if the index is less than 0 or greater or equal to the length, return null
- if the index is less than or equal to half the length of the list
  - loop through the list starting from the head and move toward the middle
  - return the node once it's found
- if the index is greater than half the length of the list
  - loop through the list starting from the tail and move towards the middle
  - return the node once it's found
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  get(index) {
    if (index < 0 || index >= this.length ) return null;
    let count, current;
    if (index <= this.length / 2) {
      count = 0;
      current = this.head;
      while (count != index) {
        current = current.next;
        count++;
      }
      return current;
    } else {
      count = this.length - 1;
      current = this.tail;
      while (count != index) {
        current = current.prev;
        count--;
      }
      return current;
    }
  }
}
```

### set()
psuedocode:
- create a variable which is the result of the **get** method at the index passed to the function
  - if the **get** method returns a valid node, set the value of that node to be the value passed to the function
  - return true
- otherwise, return false
```js
class DoublyLinkedList {
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
psuedocode:
- if the index is less than zero or greater than or equal to the length, return false
- if the index is 0, **unshift**
- if the index is the same as the length, **push**
- use the **get** method to access the index - 1
- set the next and prev proerties on the correct nodes to link everything together
- increment the length
- return true
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  insert(index, val) {
    if (index < 0 || index >= this.length) return false;
    if (index === 0) return !!this.unshift(val);
    if (index === this.length) return !!this.push(val);

    let beforeNode = this.get(index - 1);
    let afterNode = beforeNode.next;
    let newNode = new Node(val);

    beforeNode.next = newNode;
    newNode.prev = beforeNode;
    newNode.next = afterNode;
    afterNode.prev = newNode;

    this.length++;
    return true;
  }
}
```

### remove()
psuedocode:
- if the index is less than zero or greater tha or equal to the length, return undefined
- if the index is 0, **shift**
if the index is the same as the length - 1, **pop**
- use the **get** method to retrieve the item to be removed
- update the next and prev properties to remove the found node from the list
- set next and prev to null on the found node
- decrement the length
- return the removed node
```js
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  remove(index) {
    if (index < 0 || index >= this.length) return undefined;
    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    let removed = this.get(index);
    let beforeRemoved = removed.prev;
    let afterRemoved = removed.next;

    beforeRemoved.next = afterRemoved;
    afterRemoved.prev = beforeRemoved;
    removed.next = null;
    removed.prev = null;

    this.length--;
    return removed;
  }
}
```

## big O of doubly linked lists

method      | big O
------------|--------
insertion   | O(1)
removal     | O(1)
searching   | O(n)
access      | O(n)

technically, searching is O(n/2), but that's still O(n)

### recap
- doubly linked lists are almost identical so singly linked lists except there's an additional pointer to previous nodes
- better than singly linked lists for finding nodes and can be sone in half the time
- however, they do take up more memory considering the extra pointer

## final form:
```js
class Node {
  constructor(val) {
  this.val = vall;
  this.next = null;
  this.prev = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(val) {
    let newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }
    this.length++;
    return this;
  }

  pop() {
    if (!this.head) return undefined;
    let poppedNode = this.tail;
    if(this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.tail = poppedNode.prev;
      this.tail.next = null;
      poppedNode.prev = null;
    }
    this.length--;
    return poppedNode;
  }

  shift() {
    if (this.length === 0) return undefined;
    let oldHead = this.head;
    if (length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.head = oldHead.next;
      this.head.prev = null;
      oldHead.next = null;
    }
    this.length--;
    return oldHead;
  }

  unshift(val) {
    let newNode = new Node(val);
    if (this.length === 0) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.head.prev = newNode;
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }

  get(index) {
    if (index < 0 || index >= this.length ) return null;
    let count, current;
    if (index <= this.length / 2) {
      count = 0;
      current = this.head;
      while (count != index) {
        current = current.next;
        count++;
      }
      return current;
    } else {
      count = this.length - 1;
      current = this.tail;
      while (count != index) {
        current = current.prev;
        count--;
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
    if (index < 0 || index >= this.length) return false;
    if (index === 0) return !!this.unshift(val);
    if (index === this.length) return !!this.push(val);

    let beforeNode = this.get(index - 1);
    let afterNode = beforeNode.next;
    let newNode = new Node(val);

    beforeNode.next = newNode;
    newNode.prev = beforeNode;
    newNode.next = afterNode;
    afterNode.prev = newNode;

    this.length++;
    return true;
  }

  remove(index) {
    if (index < 0 || index >= this.length) return undefined;
    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    let removed = this.get(index);
    let beforeRemoved = removed.prev;
    let afterRemoved = removed.next;

    beforeRemoved.next = afterRemoved;
    afterRemoved.prev = beforeRemoved;
    removed.next = null;
    removed.prev = null;

    this.length--;
    return removed;
  }
}
```




















