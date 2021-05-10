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
