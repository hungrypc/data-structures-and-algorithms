# singly linked list

what is it?
it's a data structure that contains a **head, tail, and length** property. linked lists consists of nodes, and each **node** has a **value** and a **pointer** to another node or null
- there is no index so if you want to access a specific node, you start from the beginning and continually ask for the next node until you hit the node you were looking to access
- **singly linked** means that each node is only connected in one direction (the next node)

## comparisons with arrays

lists:
- do not have indexes
- connected via nodes with a **next** pointer
- random accesss is not allowed

arrays:
- indexed in order
- insertion and deletion can be expensive
- can quickly be accessed at a specific index

## starter code
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

  }
}

let list = new SinglyLinkedList();

let first = new Node(1);
```


















