# dijkstra's algorithm

finding the shortest path. to do this, we need a weighted graph

### starter code
```js
class WeightedGraph {
  constructor() {
    this.adjacencyList = {};

  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) {
      this.adjacencyList[vertex] = [];
    }
  }

  addEdge(v1, v2, weight) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1].push({
        node: v2,
        weight
      });
      this.adjacencyList[v2].push({
        node: v1,
        weight
      });
    }
  }

  removeEdge(v1, v2) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1] = this.adjacencyList[v1].filter(e => e.node !== v2);
      this.adjacencyList[v2] = this.adjacencyList[v2].filter(e => e.node !== v1);
    }
  }

  removeVertex(vertex) {
    if(this.adjacencyList[vertex]) {
      for (const v in this.adjacencyList) {
        this.removeEdge(vertex, v);
      }
      delete this.adjacencyList[vertex];
    }
  }
}
```

### walking through the algo
approach:
1. every time we look to visit a new node, we pick the node with the smallest known distance to visit first
2. once we've moved to the node we're going to visit, we look at each of its neighbors
3. for each neighboring node, we calculate the distance by summing the total edges that lead to the node we're checking *from the starting node*
4. if the new total distance to a node is less than the previous total, we store the new shorter distance for that node


### simple priority queue
```js
class PriorityQueue {
  constructor(){
    this.values = [];
  }
  enqueue(val, priority) {
    this.values.push({val, priority});
    this.sort();
  }
  dequeue() {
    return this.values.shift();
  }
  sort() {
    this.values.sort((a, b) => a.priority - b.priority);
  }
}
```
notice we are sorting, which is O(n logn)


### writing the algo
psuedocode:
- this function should accept a starting and ending vertex
- create an object (called distances) and set each key to be every vertex in the adhacency list with a value of infinity, except for the starting vertex which should have a value of 0
- after setting a value in the distances object add each vertex with a priority of infinity to the priority queue, except the starting vertex, which should have a priority of 0 because that's where we begin
- create another object called previous and set each key to be every vertex in the adjacency list with a value of null
- start looping as long as there is anything in the priority queue
  - dequeue a vertex from the priority queue
  - if that vertex is the same as the ending vertex - we are done
  - otherwise, loop through each value in the adjacency list at that vertex
    - calculate the distance to that vertex from the starting vertex
    - if the distance is less than what is currently stored in our distances object
      - updated the distances object with new lower distance
      - update the previous object to contain that vertex
      - enqueue the vertex with the total distance from the start node
```js
class WeightedGraph {
  constructor() {
    this.adjacencyList = {};

  }

  dijkstra(start, end) {
    const nodes = new PriorityQueue();
    const distances = {};
    const previous = {};
    let results = [];
    let current;

    // build up initial state
    for (let vertex in this.adjacencyList) {
      if (vertex === start) {
        distances[vertex] = 0;
        nodes.enqueue(vertex, 0);
      } else {
        distances[vertex] = Infinity;
        nodes.enqueue(vertex, Infinity);
      }
      previous[vertex] = null;
    }

    while (nodes.values.length) {
      current = nodes.dequeue().val;
      if (current === end) {
        while (previous[current]) {
          results.push(current);
          current = previous[current];
        }
        break;
      }
      if (current || distances[current] !== Infinity) {
        for (let n in this.adjacencyList[current]) {
          let nextNode = this.adjacencyList[current][n];
          // calculate new distance to neighboring node
          let candidate = distances[current] + nextNode.weight;
          let nextNeighbor = nextNode.node;
          if(candidate < distances[nextNeighbor]) {
            // updating new smallest distance to neighbor
            distances[nextNeighbor] = candidate;
            // updating previous - how we got to neighbor
            previous[nextNeighbor] = current;
            // enqueue in priority queue with new priority
            nodes.enqueue(nextNeighbor, candidate);
          }
        }
      }
    }
    return results.concat(current).reverse();
  }
}
```

### upgrading our priority queue to binary heap

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
          (swap && rightChild.priority < leftChild.priority)
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


## final form
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
          (swap && rightChild.priority < leftChild.priority)
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

class WeightedGraph {
  constructor() {
    this.adjacencyList = {};

  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) {
      this.adjacencyList[vertex] = [];
    }
  }

  addEdge(v1, v2, weight) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1].push({
        node: v2,
        weight
      });
      this.adjacencyList[v2].push({
        node: v1,
        weight
      });
    }
  }

  removeEdge(v1, v2) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1] = this.adjacencyList[v1].filter(e => e.node !== v2);
      this.adjacencyList[v2] = this.adjacencyList[v2].filter(e => e.node !== v1);
    }
  }

  removeVertex(vertex) {
    if(this.adjacencyList[vertex]) {
      for (const v in this.adjacencyList) {
        this.removeEdge(vertex, v);
      }
      delete this.adjacencyList[vertex];
    }
  }

  dijkstra(start, end) {
    const nodes = new PriorityQueue();
    const distances = {};
    const previous = {};
    let results = [];
    let current;

    // build up initial state
    for (let vertex in this.adjacencyList) {
      if (vertex === start) {
        distances[vertex] = 0;
        nodes.enqueue(vertex, 0);
      } else {
        distances[vertex] = Infinity;
        nodes.enqueue(vertex, Infinity);
      }
      previous[vertex] = null;
    }

    while (nodes.values.length) {
      current = nodes.dequeue().val;
      if (current === end) {
        while (previous[current]) {
          results.push(current);
          current = previous[current];
        }
        break;
      }
      if (current || distances[current] !== Infinity) {
        for (let n in this.adjacencyList[current]) {
          let nextNode = this.adjacencyList[current][n];
          // calculate new distance to neighboring node
          let candidate = distances[current] + nextNode.weight;
          let nextNeighbor = nextNode.node;
          if(candidate < distances[nextNeighbor]) {
            // updating new smallest distance to neighbor
            distances[nextNeighbor] = candidate;
            // updating previous - how we got to neighbor
            previous[nextNeighbor] = current;
            // enqueue in priority queue with new priority
            nodes.enqueue(nextNeighbor, candidate);
          }
        }
      }
    }
    return results.concat(current).reverse();
  }
}

var graph = new WeightedGraph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
graph.addVertex("D");
graph.addVertex("E");
graph.addVertex("F");

graph.addEdge("A","B", 4);
graph.addEdge("A","C", 2);
graph.addEdge("B","E", 3);
graph.addEdge("C","D", 2);
graph.addEdge("C","F", 4);
graph.addEdge("D","E", 3);
graph.addEdge("D","F", 1);
graph.addEdge("E","F", 1);
console.log(graph.dijkstra('A', 'E'));
```
