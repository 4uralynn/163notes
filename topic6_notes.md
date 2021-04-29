Topic 6: Hash Tables
====================

***"Table" Abstract Data Types***
+  Works by value rather than position
+ Implemented usuing *various* data structures, such as
  - arrays
  - LLL
  - non-linear linked lists

___

**MAIN FOCUS**
*Arrays of Linear Linked Lists*
___

***Table ADTs*** manage data by its value!
+ As with the other ADTs, table operations can be implemented with both arrays and LLLs
+ *Value Oriented* ADTs  allolws you to
+ **Insert** data containing a certain ***KEY*** value into a data structure
+ **Delete** a data item containing a certain ***KEY*** value from a data structure
+ **Retrieve data using a ***KEY VALUE*** from the client and find out if the structure is empty or full
+ Similar to Python dictionaries... or whats going on under the hood with Python dictionaries
+ Designed to look up information by various search *keys*

___
BASIC OPERATIONS FOR TABLE ADTs:

  - Create an empty table: `Create(Table)`
  - Insert an item into the table: `Insert(Table, Newdata)`
  - Delete an item from the table: `Delete(Table, Key)`
  - Retrieve an item from a table: `Retrieve(Table, Key, Returneddata`
    * **NOT** Display

### Table ADT Efficiency

|    *Type*          |                         Add                       |                Remove               |        Search             |            Display (Retrieval)         |
|--------------------|---------------------------------------------------|-------------------------------------|---------------------------|----------------------------------------|
|  **Sorted Array**  |        + Binary Search, - Shifting , - Memory     |     + Binary Search, - Shifting     |      + Binary Search      |            + Direct Access             | 
| **Unsorted Array** |    + Direct Access, + **NO** Shifting, - Memory   | - **Sequential** Search, - Shifting |  - **Sequential** Search  | - *Must* implement a sorting algorithm |
|     Sorted LLL     | - Sequential Search, + No Shifting, + Flex w/ Mem | - **Seq** Srch, + **NO** Shft, + Stop any time | - **Seq** Srch |               + Supported              |
|    Unsorted LLL    | + Dir Accss, + **NO** Shft, + Flexibility w/ Mem  |    - Seq Srch, + **NO** Shft, +Flex w/ mem     | - **Seq** Srch |	- *Must* implement a sorting algoritm  |
| ***Hash Table Using Chaining*** | ***+ Instantaneous, + Direct Access, + Flexibility with Memory*** |     **"**         |      **"**     | - Not Available (use a different data structure)|

___
**NOTE:**

Read the Carrano textbook, *Data Abstraction and Problem Solving with C++*, on **hash tables**. 
Many test quesions will come from the book." *(Chapter 18.4)*

___

In a **Hash Table**, function translates the key into an array index.
+ Table size should be a *prime* number
+ Function should work with a number larger than the table size so it can be modded (%)
  - Remainder becomes index
+ We will be doing very simple hash functions, developed on our own
+ array *must* be initialized so `node *head = NULL`

***Collision*** is when two different keywords collide at the same index.
+ In a **perfect hash function**, there are no collisions. (Not expected in this course)
+ Must learn **collision** ***resolution*** **techniques.**
  -  Chaining: `Add()` will insert at the head of a chain even if there is a collision (array of head pointers).
     * Chains are not ordered
     * Distribute evenly. Test out different hash functions.
     * *ALWAYS* insert at the beginning (similar to a stack, but an array of LLL, instead of a LLL of arrays)
     * length of the chain tells how many collisions have happened
     * performance of ***O***<sub>n</sub> ... n = chain length

##### Constructing a Hash Table

```c++

hashtable::hashtable();
{
	node ** hshtable;
	hshtable = new node*[SIZE]
	for (int i = 0; i < SIZE; ++i) {
		hshtable[i] = NULL;
}

```

___
**NOTES:**

 * A hash table cannot display but random data. This is where it falls short and is not the right structure for displaying data.
 * Will be in Program 3 and Lab 6.
 * We will not be using multiple hash functions, but it is common.
___


