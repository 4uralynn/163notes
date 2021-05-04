Topic 8: Tree Introduction
==========================

Part 1: Terminology
-------------------

**Learning Goals**
+ Trees 
  - New non-linear structure, table ADT
+ Organizing data in a hierarchal fashion
+ Applying recursion


***Table ADT Review***
+ None of the methods for implementing tables were really adequate
+ With many applications, operations are not as efficient as necessary
+ Hasing is good for retrieval, but can't obtain a sorted list of information

#### Tree Terminology

**Trees** are used to represent the relationship between data items.
+ All trees are hierarchal 
  - parent/child relationship between nodes
+ Lines between nodes are called *directed edges*
+ If there is a directed edge from node **A** to node **B** -- then ***A*** is the parent of **B** and **B** is a child of ***A***
+ In a *binary* tree, each parent node can have at most two children
+ Single direction [***A*** to **B**, but not **B** to ***A*** (see representation)]
+ Childen of the same parent are called *siblings* (**B** and **C** are siblings of ***A***)

##### *Respresentation:*
```
	A
	^
      /   \
     B     C
     ^     ^
    / |   / \
   D  E   F  G
   ^  ^   ^  ^
  / || \ / \ |\ 
 H  IJ K L M N O

{... and so on...}

```
**Root** is the only node in the tree with *no parent*.

**Leaf** is a node with no children.

**Siblings** are nodes with a common parent.

***Ancestor*** **of** ***n*** is a node on the path from the *root* to *n*.

***Decendant*** **of** ***n*** is a node on a path from *n* to a *leaf*

**Empty Tree** is a tree with nodes!

**Subtree of** ***n*** is a tree that consists of a *child of n* and the *child's* ***descendants***.

**Height** the number of nodes on the longest path from *root* to a *leaf*.

***Binary*** **Tree** is a tree in which each node has, at most, two children.

***Full*** **Binary Tree** is a binary tree *of height h* whose leaves are all at the level *h* and *whose nodes all have two children*. This is considerted to be **completely balanced.** *(above representation is a full binary tree)*
  - A *full* tree is also a *complete* tree.
***Complete*** **Binary Tree** is a binary tree that is a *full* tree *at a level below* its height (*h - 1*)

#### Binary Trees
+ While traversing downward, for every node, there are either no children (this node is a *leaf*), or two children called left and right *subtrees*.
  - A *subtree* is a subset of a tree including some node in the tree and all its decendants.
  - `node *left;` and `node *right`
+ **Binary Search Tree** (**BST**), sorted to the according to values in the nodes
  - Allows traversal/data-retrieval in *sorted order*
  - For each node *n*, all values greater than *n* are located in the left of the subtree. All values less than *n* are located in the left.
    * Both trees are considered binary trees themselves
    * Equal values can go either left or right, but the paradigm should be known/agreed ahead of implementation.
  - Data is organized in a way that facilitates ***searching*** the tree for a particular data item.
    * Ends up solving the problems of sorted-traversal with *linear implementations of the ADT table*
    * If *reasonably* balanced (*full* or *complete* tree), it can provide logarithmic (***O****(log<sub>2</sub>N)*) retrieval, removal, and insertation performance. 

___
**NOTES:**

Read the Carrano texbook -- Two chapters on trees.
*Read the first chapter before lab*

___


Part 2: Traversal
-----------------

Just like other ADTs, a binary tree can be implemented using *pointers* or *arrays*.

*For pointer implementation:*

```c++

struct node {
	data value;
	node * left_child;
	node * right_child;
};

```

Facilitate **Pointers to Data**:
+ when more than a single data structure needs to reference the same tree
+ when we are not replicating data
+ perhaps the data is a *head* pointer to a LLL, or a pointer to root, or to another tree
  - each node's data is actually a list of items

```c++

struct node {
	//(other ptrs)
	data_type * ptr_value;
};

```

***Implementation of a Binary Tree***
+ choice of using *iteration* or *recursion* and still have reasonably efficient results
+ If the tree is reasonably balanced, we can traverse with a minimal number of recursive calls

```c++
//Instead of 'binary_tree', we will use 'table'.
class binary_tree {
	public:
		binary_tree();
		~binary_tree();
		int insert(const data &);
		int remove(const key &);
		int retrieve (const key &, datatype [], int & num_matches);
		int display();
	private:
		node * root;
};

```
**Traversal Algorithms**
+ Preorder:
  - Traverse(root)
    * If the tree is not empty then
      1. Visit the node at the root *(display)*
      2. Traverse(left subtree)
      3 Root
      4. Traverse(right subtree)
+ Postorder
  - Traverse(root)
    * If the tree is not empty then
      1. Visit node at root
      2. Traverse(left subtree)
      3. Traverse(right subtree)
      4. Root

___
**NOTE:**

Code in the textbooks uses *pointers to functions*, which will not be used until CS202

___

***Example Traversal Algorithm:***

```c++

#include <iostream>
#include <cstring>
#include <cctype>
using namespace std;

struct node
{
	int data;
	node * left;
  	node * right;
};

//Prototypes
void build(node * & root);
void display(node * root);
void destroyall(node *& root); 		//will write
int display_inorder(node *root); 	//will write

//main
int main();
{
	node * root = NULL;
	build(root);
	display(root);

	int count = display_inorder(root); 		//function calls
	cout endl << "Our count value was: " << count << endl;
	destroyall(root);
}

//Function Implementation                                  Examples of coding traversal:
int display_inorder(node * root)
{
	if (!root) return 0; //empty tree or end of path
	
	//Inorder traversal
	int count = 0;
	count = display_inorder(root->left);
	++ counter;
	cout << root->data << " ";
	count += display_inorder(root->right);
	return count;
}

//Postoder traversal 
void destroyall(node *& root)
{
	if (!root) return;
	destroy(root->left);
	destroy(root->right);
	delete root;
	root = NULL;
}

```


