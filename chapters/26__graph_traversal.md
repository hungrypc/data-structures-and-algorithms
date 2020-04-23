# graph traversal

graph traversal uses:
- peer to peer networking
- web crawlers
- finding 'closest' matches/recommendations
- shortest path problems
  - GPS navigation
  - solving mazes
  - ai (shortest path to win the game)

## depth first search
when you move from node to node, one by one

### recursive
psuedocode:
- the function should accept a starting node
- create a list to store the end result, to be retured at the very end
- create an object to store visited vertices
- create a helper function which accepts a vertex
  - the helper function should return early if the vertex is empty
  - the helper function should place the vertex it accepts into the visited object and push that vertex into the result array
  - loop over all of the values in the adjacencyList for that vertex
  - if any of those values have not been visited, recursively invoke the helper function with that vertex
```js
/*
DFSr(vertex):
  if vertex is empty
    return (base case)
  add vertex to results list
  mark vertex as visited
  for each neighbor in vertex's neighbors:
    if neighbor is not visited:
      recursively call DFS on neighbor
*/
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  DFSr(start) {
    let results = [];
    let visited = {};
    const adjacencyList = this.adjacencyList;

    (function helper(vertex) {
      if (!vertex) return null;
      visited[vertex] = true;
      results.push(vertex);
      adjacencyList[vertex].forEach(value =>  {
        if (!visted[value]) return helper(value);
      });
    })(start);
    return results;
  }
}
```

### iterative
psuedocode:
- the function should accept a starting node
- create a stack to help use keep track of vertices (list/array)
- create a list to store the end result to be returned at the end
- create an object to store visited vertices
- adding ths starting vertex to the stack, and mark it visited
- while the stack has something in it
  - pop the next vertex from the stack
  - if the vertex hasn't been visited yet:
    - mark it as visited
    - add it to the reults list
    - push all of its neighors into the stack
- return the result array
```js
/*
DFSi(start):
  let S be a stack
  S.push(start)
  while S is not empty
    vertex = S.pop()
    if vertex is not labeled as discovered:
      visit vertex (add to result list)
      label vertex as discovered
      for each of vertex's neighbors, N do
        S.push(N)
*/
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  DFSi(start) {
    let S = [start];
    let result = [];
    let visited = {};
    let vertex;
    visted[start] = true;

    while (S.length) {
      vertex = S.pop();
      result.push(vertex);

      this.adjacencyList[vertex].forEach(n => {
        if (!visited[n]) {
          visited[n] = true;
          S.push(n);
        }
      });
    }
    return result;
  }
}
```


### breadth first search
when you visit all the neighbors of the node you're on before moving on and doing the same to the next node

psuedocode:
- this function should accept a starting vertex
- create a queue (use an array) and place the starting vertex in it
- create an object to store nodes visited
- mark starting vertex as visited
- loop as long as there is anything in the queue
- remove the first vertex from the queue and push it into the array that stores nodes visited
- loop over each vertex in the adgacency list for the vertex you are visiting
- if it is not inside the object that stores nodes visited, mark it as visited and enqueue that vertex
- once you finish looping, return the array of visited nodes
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  BFS(start) {
    let queue = [start];
    let visited = {};
    let result = [];
    let vertex;
    visted[start] = true;

    while (queue.length) {
      vertex = queue.shift();
      result.push(vertex);
      this.adjacencyList.forEach(n => {
        if (!visited[n]) {
          visited[n] = true;
          queue.push(n);
        }
      });
    }
    return result;
  }
}
```


## final form
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) {
      this.adjacencyList[vertex] = [];
    }
  }

  addEdge(v1, v2) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1].push(v2);
      this.adjacencyList[v2].push(v1);
    }
  }
  removeEdge(v1, v2) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1] = this.adjacencyList[v1].filter(e => e !== v2);
      this.adjacencyList[v2] = this.adjacencyList[v2].filter(e => e !== v1);
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