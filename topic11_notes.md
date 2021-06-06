Topic 11: Graphs and Heaps
===============

Moving from Trees to Graphs
---------------------------
+ Trees are built on hierarchal relationships. but there are often more complex relationships
+ Graphs are built on complex relationships

Graphs
------
+ The last ADT we will learn about
+ Represent how data can be related to one another... setting up an inherant structure.

**Terminology**
+ Graphs use ***vertices*** (not nodes) and ***edges***
+ A ***path*** is a sequence of edges from one vertex to another.
+ Paths may pass through the same vertex more than once, but a **simple path** may not.
+ A **cycle** is a path that starts and ends at the same vertex, but won't pass other vertices more than once
+ A **connected** graph means there is a path between every pair of vertices
+ **Complete** means there is an *edge* between every pair of vertices.
+ Edges can have lables -- numeric values -- creating a **weighted graph**
+ **Weights** can be the distances between vertices. 
+ In **directed** graphs, edges are directional. (A to B is not the same as B to A).

*ADT Graph Operations might include:*
+ Create an empty graph
+ determine if the graph is empt
+ insert a vertex
+ insert an edge between two vertices
+ delete a vertex
+ delete an edge between two vertices
+ retrieve the value of the data at a vertex
+ replace data at a particular vertex
+ deteremine if there is an edge between two vertices

*Operations are often tailored to the application.*

**One common way of implementing a graph** is to uses an ***adjacency list***
+ An array of vertices, with an **edge list**, and array of visit flags
+ Consists of *N* linked lists
+ There is a node of list *i* for vertex *j* if and only if there is an edge from vertex *i* to *j*
+ edge list is the *vertices a particular vertex is adjacent to*

#### Traversal Algorithms
1. Depth first 
  1. Start at any vertex
  2. Return if no vertex in edge list or if vertex has been visited
  3. Start loop. If vertex in edge list, set visit flag, call function with new vertex
  4. (Unset visit flags?)
2. Breadth first
  1. Start at any vertex
  2. Return if no vertex in edge listmor vertex has been visited  
  3. Start loop of adjacents, set visit flag. 
  4. Start loop with function call for each iterated vertex
  5. (Unset visit flags?)


Heaps
-----

A heap is a data structure similar to a BST, but ***unsorted***.
+ Heaps are always complete binary trees 
  - full tree at *h - 1*, and leaves filled from left to right
+ We always know what the maximum size of a head is.
+ value of each node in a head is greater than or equal to the value of each of its children
+ No relationship between data values of the children (either could be the larger value)
+ Heaps are used to implement *priority queues*.
  - A ***Priority Queue*** is an ADT

#### Priority Queue ADT
+ Think of a to-do list, where each item has a priority value which relects the urgency with which each item needs to be addressed
+ Determines which item is the next highest priority
+ Maintains items sorted in **descending order** -- inverse priority
  - Item with the highest priority is always at the top of the list
+ A "weaker binary tree" but sufficient for the efficient performance of priority queue operations

**Removing from a Heap**
+ Remove the largest data item (highest priority), *the root*
+ Return to calling routine
+ Compare child data

##### Heapsort
1. Enter all data to the tree
2. Sort afterward, compare nodes


