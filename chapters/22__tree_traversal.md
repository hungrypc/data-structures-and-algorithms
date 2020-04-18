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


