# Graphs

* A graph is a non-linear data structure that can be looked at as a collection of vertices (or nodes) potentially connected by line segments named edges.

* some common terminology used when working with Graphs:

1. Vertex - A vertex, also called a “node”, is a data object that can have zero or more adjacent vertices.
2. Edge - An edge is a connection between two nodes.
3. Neighbor - The neighbors of a node are its adjacent nodes, i.e., are connected via an edge.
4. Degree - The degree of a vertex is the number of edges connected to that vertex.

***Undirected Graphs***

* An Undirected Graph is a graph where each edge is undirected or bi-directional. This means that the undirected graph does not move in any direction.

***Directed Graphs (Digraph)***

* A Directed Graph also called a Digraph is a graph where every edge is directed.

* Unlike an undirected graph, a Digraph has direction.
* Each node is directed at another node with a specific requirement of what node should be referenced next.

* There are many different types of graphs. This depends on how connected the graphs are to other node/vertices.
* The three different types are :

1. completed
2. connected
3. disconnected

***Complete Graphs***

* A complete graph is when all nodes are connected to all other nodes.

***Connected***

* A connected graph is graph that has all of vertices/nodes have at least one edge.

***Disconnected***

* A disconnected graph is a graph where some vertices may not have edges.

## Acyclic vs Cyclic

* In addition to undirected and directed graphs, we also have acyclic and cyclic graphs.

***Acyclic Graph***

* An acyclic graph is a directed graph without cycles.

* A cycle is when a node can be traversed through and potentially end up back at itself.
* A directed acyclic graph is also called a DAG.

***Cyclic Graphs***

* A Cyclic graph is a graph that has cycles.

* A cycle is defined as a path of a positive length that starts and ends at the same vertex.

## Graph Representation

* We represent graphs through:

1. Adjacency Matrix
2. Adjacency List

***Adjacency Matrix***

* An Adjacency matrix is represented through a 2-dimensional array. If there are n vertices, then we are looking at an n x n Boolean matrix.
* a sparse graph is when there are very few connections. a dense graph is when there are many connections
* Within an adjacency matrix, an undirected graph will always be symmetric.

***Adjacency List***

* An adjacency list is the most common way to represent graphs.

* An adjacency list is a collection of linked lists or array that lists all of the other vertices that are connected.

* Adjacency lists make it easy to view if one vertices connects to another.

***Weighted Graphs***

* A weighted graph is a graph with numbers assigned to its edges. These numbers are called weights.

## Traversals

* The traversals itself are like those of trees.

***Breadth First***

* you will starting at a specific vertex/node. This node must be specified when calling the BreadthFirst() method.
* Traversing a graph that has cycles will result in an infinite loop. to To prevent we will add the node we visit to visited set.

* we can use Breadth First by :

1. Enqueue the declared start node into the Queue.
2. Create a loop that will run while the node still has nodes present.
3. Dequeue the first node from the queue
4. if the Dequeue‘d node has unvisited child nodes, add the unvisited children to visited set and insert them into the queue.

***Depth First***

* we using a Stack for our depth-first traversal.
* we can use it by :

1. Push the root node into the stack
2. Start a while loop while the stack is not empty
3. Peek at the top node in the stack
4. If the top node has unvisited children, mark the top node as visited, and then Push any unvisited children back into the stack.
5. If the top node does not have any unvisited children, Pop that node off the stack
6. repeat until the stack is empty.

## Real World Uses of Graphs

* Graphs are extremely popular when it comes to it’s uses.
* examples of graphs in use:

1. GPS and Mapping
2. Driving Directions
3. Social Networks
4. Airline Traffic
5. Netflix uses graphs for suggestions of products
