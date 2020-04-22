# graphs

a **graph data structure** consists of a fininte (and possibly mutible) set of vertices or nodes or points, together with a set of unordered pairs of these vertices for an undirected **graph** or a set of ordered pairs for a directed graph
- what?
  - a graph is a collection of nodes and connections between those nodes (like the graphql logo)

the difference between trees and graphs:
- in trees, nodes are connected by exactly one path
- in graphs, nodes can be connected by multiple paths

### uses for graphs
- social networking
- location/mapping
- routing algorithms
- visual hierarchy
- file system optimizations
- basically everywhere

### terminology
- vertex: a node
- edge: connection between nodes
- weighted/unweighted: values assigned to distances between vertices
  - unweighted: edges have no value assigned to them
  - weighted: edges have value assigned (info about the connection itself)
- directed/undirected: directions assigned to distances between vertices
  - undirected: no direction to the edges (two way connections)
  - directed: particular direction to edges (one way connection)

### storing graphs
two approaches:

1. adjacency matrix:
- a two dimensional structure, usually implemented with nested arrays
- we store information in rows and columns
  - (con) takes up more space (in sparse graphs)
  - (con) slower to iterate over all edges
  - (pro) faster to lookup specific edge
2. adjacency list:
- using an array or list to store the
  - (pro) can take up less space (in sparse graphs)
  - (pro) faster to iterate over all edges
  - (con) can be slower to lookup specific edge

### differences and big O
- v = number of vertices
- e = number of edges

operation      | adjacency list | adjacency matrix
---------------|----------------|-----------------
add vertex     |O(1)            |O(v^2)
add edge       |O(1)            |O(1)
remove vertex  |O(v + e)        |O(v^2)
remove edge    |O(e)            |O(1)
query          |O(v + e)        |O(1)
storage        |O(v + e)        |O(v^2)


we will be using an adjacency list

### starter code
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
  }
}
```

### add vertex
psuedocode:
- write a function called addVertex which accepts a name of a vertex
- it should add a key to the adjacency list with the name of the vertex and set its value to be an empty array
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
}
```

### add edge
psuedocode:
- this function should accept two vertices,vertex1 and vertex2
- the function should find in the adjacency list the key of vertex1 and push vertex2 to the array
- the function should find in the adjacency list the key of vertex2 and push vertex1 to the array
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  addEdge(v1, v2) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1].push(v2);
      this.adjacencyList[v2].push(v1);
    }
  }
}
```

### remove edge
psuedocode:
- this function should accept two vertices
- reassign the key of v1 to be an array that doesn't contain v2
- reassign the key of v2 to be an array that doesn't contain v1
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  removeEdge(v1, v2) {
    if(Object.keys(this.adjacencyList).includes(v1 && v2)) {
      this.adjacencyList[v1] = this.adjacencyList[v1].filter(e => e !== v2);
      this.adjacencyList[v2] = this.adjacencyList[v2].filter(e => e !== v1);
    }
  }
}
```

### remove vertex
psuedocode:
- this function should accept a vertex to remove
- loop through as long as there are any other vertices in the adjacency list for that vertex
- inside the loop, call our removeEdge function with the vertex we are removing and any values in the adjacency list for that vertex
- delete the key in the adjacency list for that vertex
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
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
