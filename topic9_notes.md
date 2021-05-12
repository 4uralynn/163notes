Topic 9: Binary Search Trees
============================

Part 1 : Tree Insertion
-----------------------

***Foundations***
1. Remember, *insert* **always** inserts data at a leaf
2. Similar to inserting data at the end of a linear linked list
   + Good news is that we don't have to special case the situation where we are trying to rearrange pointers, inserting in the middle.

```c++

//Add node to end of LLL
void add_end(node *& head), int new_data)
{
	if (!head) {
		head = new node;
		head->data = new_data;
		head->next = NULL;
		return;
	}
	add_end(head->next, nex_data);
}

//More like C, where we don't have pass by reference
node * add_end(node * head), int new_data)
{
	if (!head) {
		head = new node;
		head->data = new_data;
		head->next = NULL;
		return head;
	}
	head->next = add_end(head->next, nex_data);
	return head;
}


void add_end(node ** head), int new_data)
{
	if (phead && !(*phead)) {
		*phead = new node;
		(*phead)->data = new_data;
		(*phead)->next = NULL;
		return;
	}
	add_end(&(*phead)->next, nex_data);
}

```

How does this apply to Binary Search Trees?
- You always add at the leaf.

```c++

//Recursive insert for BST
void insert_BST(node *& root, int new_data)
{
	if (!root) {		//Root is NULL(empty or finished traversing)
		root = new node;
		root->data = new_data;
		root->left = root->right = NULL;
		return;
	}
	if (new_data < root->data) //go left
		insert_BST(root->left, new_data);
	else
		insert_BST(root->right, new_data);
}

```

**The only thing different** from this and the above code for LLL is, the extra pointer (Left/right), and the recursive call is split in two directions (left/right, if/else).

Part 2: Removal
---------------

**With removal, you can remove** ***anywhere!***

Implement *case by case*, building *incrementally*.
1. Retrieve
   - learn how to find data in the tree.
2. No match 
   - recursive `root` alias is NULL
3. Match is leaf (delete the node and set to NULL)
   - `if (!root->left && !root->right)`
4. Match is a child w/ child (parent 'adopts' child)
   - `else if (!root->left && root->right)`
     * adopt by `hold = root->right; delete root; root = hold;`	
   - `else if (!root->right && root->left)`	
     * adopt by `hold = root->left; delete root; root = hold;`	
5. Match is a child w/ 2 children (finds *In Order Successor* (IOS)
   - find IOS. `else` 
   - `while (current->left = NULL)`
     * move data to root alias node
     * adopt by `hold = current->right; delete current; curren = hold;`	
     * delete node of IOS


Part 3 : Coding Examples
------------------------

**Counting** the leaves with *preorder traversal*

```c++

#include "table.h"

//Count the number of nodes with no children
//return the count
//PREORDER traversal
int count_leaf(node * root)
{
	//Base
	if (!root) return 0;
	//Am I a leaf? -- If so, count it and stop
	if (!root->left && !root->right)
		return 1;
	
	//Otherwise
	/* int count = count_leaf(root->left);
   	count += count_leaf(root->right);
	return count; */
     	return count_leaf(root->left) + count_leaf(root->right);
}

```

**Display** even data wint *in order traversal*

```c++

//Display all even, return the sum of all data displayed
//IN ORDER traversal
int display_even(node * root)
{
	//base case
	if (!root) return 0;
	//Inorder traversal (left - then visit node - the right)
	int sum = display_even(root->left);
	if (root->data % 2 == 0) { //even
		cout << root->data << '-';
		sum += root->data;
	}
	return sum += display_even(root->right);
}

```

**Count data**, only if both children are even, with *postorder traversal*.

```c++

//Count the number of items that have even data as children
//POSTORDER traversal
bool count_child(node * root, int & count)
{	
	//base case
	if (!root) return true;
	//left, then right, then visit the node (handle children first)
	bool left = count_child(root->left, count));
	bool right = count_child(root->right, count));
	if (left && right) ++count;
	//visit the node... if even, return true
	if (root->data % 2 == 0) return true;	
	return false;
}

```

Part 4: Tree Efficiency
-----------------------

***Review***
+ Maximum height of a binary tree with *N* nodes is a height of *N*
  - An *N*-node tree with a height of N is a LLL
+ Consider:
  - I height is 3, there can be anywhere between 3 and 7 nodes in the tree.
  - Trees with more than 7 nodes will ***require*** that the height be *greater* than 3.


**Mathematical Relation/Function**
+ A full binary tree of height h should have 2 to the power of *h* nodes, minus 1, in that tree:

*2<sup>h</sup> - 1*

**Height tells you the distance** of a node from the root.
+ Determines how efficiently it can be located.
+ The shorter we can make the tree, the easier it is to locate any desired node in the tree
+ Knowing the height is important when inserting an item to the tree (maximum amount to travel)

#### To determine if a tree is *balanced*
+ Calculate the ***balance factor***
  - the difference in heights between its left and right subtrees.
  - *balance = H<sub>L</sub> - H<<sub>R</sub>*
     * Balanced if balance factor is *1, 0,* or *-1*.
     * A *full tree* has a balance factro of 0.
     * With a facor of 0, subtrees are also balanced

For efficiency, the best case is when the height is a logarithmic value (*log<sub>2</sub>N*), and worst case is when height is *N*.
+ The more balanced you are the higher degree of efficiency you have for operations
  - *retreive, insert, delete*
  - We must follow a path from the root down to the node that contains the desired data
  - Maximum number of nodes that can be on any path is equal to the number of comparisons  table operations can require
+ Balanced trees can be searched with efficiency comparable to the binary search
+ Trees that have a linear shape are no better than a linear linked list
  - So it is best to use varitions of the basic binary search tree ***with algorithms*** that can *prevent the shape of the tree from degenarating*
    * Variation include the *2-3 tree*, *2-3-4 tree*, *red-black tree*, and the *AVL tree*

___
**NOTE:**

The *2-3 tree* and *2-3-4 tree* variations are ***perfectly balanced***. They are always 100% **full trees*.
The *red-black* tree is a simulation of the first two.

___

#### The *2-3 Tree*
+ 100% balanced, 100% of the time
+ Every parent always has 2 children
  - 1 data item will mean *2 children*
  - 2 data items will mean ***3 children*** (1 singluar and 2 conjoined in an array)

___
***2-3 Tree*** **Algorithm:**

1. Add a leaf.
2. If the leaf has only 1 data item, store the new data in that node
3. If the node has 2 data items
   1. Find the middle data item
   2. Push it up (recursively)
   3. Split the node
4. Much like the *BST*, but when a node has 2 data items:
  + The *left* subtree is **less** than the smallest data item.
  + The *middle* subtree is **greater** than the smallest **but less** than the larger data item
  + The *right* subtree is **greater** than the largest data item.

___
**REMEMBER**

*A 2-3 tree is actually a* ***B tree*** *of 3rd degree.*

___

**Code for 2-3 Tree Nodes:**

```c++

struct node {
        data * array[2];   //data ** array;
        node * child[3];
};

// A total of 5 pointers (2 data pointers and 3 node pointers)

```
*Negatives to the 2-3 Tree*
+ There can be a spike in run-time performance when data needs to be recursively pushed all the way up the tree. So this may not be best for large applications expecting high run-time performance.
+ **Very** difficult to implement removal of nodes (won't learn in this course).


##### Head Recursion Coding Example
```c++

#inlude "list.h"

bool find_last2(node * head)
{
        if (!head)
                retrun false;
        bool found = find_last2(head->next);
        //Now is where th work happens
        if(!found && head->data == 2) {
                head->data = 99;
                found = true; //SUCCESS, we found it
        }
        return found;
}

```
