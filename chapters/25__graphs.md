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
2. adjacency list:
- using an array or list to store the edges

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






























