Topic 10: Balanced Trees
========================

2-3 Tree
--------

*100% Balanced, 100% of the time*

In a 2-3 tree, each node can have 1 or 2 pieces of data. 
+ If there is one piece of data, it is either a leaf, or the node has **two** children.
+ If the are two pieces of data, it is either a leaf, or there are **three** children.
+ There is **NEVER** a node with only one child

#### 2-3 Tree Insert Algorithm

1. Add at a leaf
2. If a the leaf has *only 1* data item, store the new data in that node
3. If the leaf has 2 data items,
  + Find the middle data items
  + Push it up
  + Split the node
4. When a node has **2 data items**
  + the ***left*** subtree is *less than* the smallest data item 
  + the **middle** subtree is *greater than the smallest but less than the largest* data items
  + the **right** is *greater than* the largest data item


2-3-4 Tree
----------

In a 2-3-4 tree, each node can have 1,2, or 3 pieces of data.
+ If there is one piece of data, it is either a leaf, or the node has **two** children.
+ If there are two pieces of data, it is either a leaf, or there are **three** children.
+ If there are three pieces of data, it is either a leaf, or there will be **four** children.
+ Again, there is **NEVER** a node with only one child


**Code Example for node** *(7 pointers!)*

```c++

struct node {
	data * items[3];
	node * child[4];

};

```

#### 2-3-4 Tree Algorithm

1. Travel to the appropriate leaf to add
2. As we travel down the tree, anytime a node with 3 pieces of data is encountered
  + push up the middle data item
  + split the node
  + continue traversing
3. There ***will*** **always** be room in the leaf for the new item being added
4. Provides consistent runtime performance at the cost of memory overhead.


Red-Black Tree
--------------

*A BST with color flags*, which we can use to simulate a 2-3-4 tree. There are 2 color flags per node, representing the type of relationship with the child.
+ There can be only one color flag, but book uses 2.
+ Instead of 'red' and 'black', we can flag as 'internal' or 'child'
+ Like 2-3-4 algorithm, but instead of splitting the node (with two leafs), we change the flag
+ A node can have only one child, like a normal BST


AVL Tree (admissible tree)
--------------------------

The AVL tree is a classical method proposed by Adelson-Velskii and Landis
+ Creates "admissible tree"
+ Focuses on *rebalancing the tree locally* to the portion of the tree affected by insertion and deletions
+ It allows the height of the left and right subtrees of every node to differ by *at most* one
+ Complex code with many special cases
+ Each node keeps track of the "balance factors" which records the differences between the heights of the left and right subtrees
  - Balance factor is the height of the right subtree minus the height of the left
  - All balance factors must be +1, 0, or -1.

We ***rotate*** the tree to make it balanced.
+ Rotations are not necessary after every insertion & deletion (only needed when the height differes by more than 1)
  - 78% of deletions require no rebalancing
  - 53% of insertions do not bring tree out of balance
+ Single rotations and double rotations

B-Trees
------
*(See Topic 11 on Heaps first)*

Tables stored externally can be be searched with B-Trees
+ A more generalized approach then the 2-3 tree
+ With externally stored tables, we want to keep the search tree as short as possible
  - Much faster to do extra comparisons at the node (like a heap) than to find the next node
+ Every time we want to get another node
  - We have to access the file and read in the appropriate data
  - Less time to operate within a particular node (doing comparisons) once read in
  - We should try to reduce the height of the tree even if it means doing more comparisons
+ We allow each node to have as many children as possible
+ If *m* children, then you much be able to allocate enough memory for that node to contain the data and m pointers to the node
  - The data such a node must have *m - 1* key value
+ Ideally, you structure trees so that every *internal* node has *m* children and all leaves are at the same level
+ For example, if *m* is 5, then every node should have 5 children and 4 data values
  - Difficut to maintain with variety of insertions and deletions

We can require that B-trees is balanced (like 2-3 tree), but the number of children should be between *m* and *(m/2) + 1*
+ This is a B-tree of degree *m*
  - A 2-3 tree is a B-tree of degree 3
+ Requires all leaves be at the same height
+ Algorithms are similar to the 2-3 tree or 2-3-4 tree



