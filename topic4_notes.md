Topic 4 - Stacks and Queues
===========================
Part 1
------

**Learning Goals:**
+ What are *stacks*?
  - Like Ordered Lists, are "position oriented"
+ Use of data structures for *stacks* and *queues*
  - arrays [statically (barely) and dynamically allocated]
  - LLLs
  - circular linked lists
  - Flexible arrays

___
**Remember**

Data abstraction is a technique for controlling the interaction between a program and its data structures and the operations performed on this data

It builds "walls" around a program's data structures. Such walls make programs easier to design, implement, read, and modify.
___

### Stacks
*"Only work at the top."*
+ stacks are considered the easiest type of list to use
  - no opportunity to insert
+ the only operations on stacks are to add/remove things to the **top** of the stack
+ We never need to insert, delete, or access data that is somewhere other than at the top of the stack.

**Operations**
+ When adding to top of the stack we say we are **pushing** data onto the stack
+ When removing from the top of the stack we say **popping** data from the stack
+ Sometimes we need to determine if the stack is *empty* or *full*
+ 5 important operations:
  1. Determine whether the stack is empty
  2. **PUSH** - Add a new item onto the 
  3. **POP** - Remove an item from the stack... pop
  4. Initialize a stack 
    - this op is easy to overlook
  5. *PEEK* - Karla terminology - Retrieve the item at the top of the stack, without modifying the stack
+ Other operations
  6. Destructor
  7. Display all

___
**NOTE:**

The concept of stacks comes from the concept of recursive functions. 
Every time there is another recursive call, a stack fame is *pushed* onto the program stack, and as you return from the function, that stack fram is *popped* from the top of the program stack.
___

**Implemenation**
+ Keep in mind that we should have functions to push and pop data
  - hides the implementation details from the user as to how routines actually access our memory
    * you can implement stacks using either arrays, or using linked lists w/ dynamic memory

***Code example:***
```c++
class stack {
	public:
		stack();
		~stack();
		int push(const datatype & arg_name);  //pass stucts or or class by reference (use 'const' to pass read-only)
		int pop(data & arg_name); 	//pop doesn't necesarily need an argument
		int peek(datatype & arg_name);
		int isempty(); int isfull();
		int display(); 	//optional
}
```

___
**NOTE:**

To identify **segfault** line number, *run gdb:* with `g++ [file] -g` during compile, or `gdb ./a.out` after compiling
___

Part 2
------

### Eficiency trade-offs for various structures
+ run-time performance
+ memory usage

***Arrays***
+ Push from the top *index*
+ where is the top? 
  - **start at 0 and for forward** *(expect in lab)*
    * *the position after--or on top-- or the last data indexed*
  - **or**  start at -1
+ **'Top' as an index:**
  - code: `array[top] = value; ++top;`
  - **DO NOT USE ASSIGNMENT OPERATOR** for classes, structs, or anything but a built-in data type
    * use member function `array[top].set(to_add);`
  - Review of Pointer Arithmetic - CS162 Topic
    * in `array[top]` or `*(array + top)`, *top* an `int` (integer) data type and *array* is a `ptr` (pointer). C++ does an automatice type conversion
    * use `top = array` .. which is the same as `top = &(*(array + 0))` (--&*--), to give top the address of array
    * about 9 operations to access 
+ **'Top' as a pointer

***A dynamically allocated list is batter than statically allocated*** *(one less problem)*
+ if the cost of memory allcocation for the array is manageable at run-time
+ may not be reasonable  if array sizes are very large, or *many many* stack objects
+ not required if the size of the data is known up-front at compile time (and same for each instance of the class)

***Linear Linked List***
```c++
	private:
		node * head;
		node * tail;  //not helpful for a stack at all (working from the top)
```
___
**NOTE:**
**Where is the *top*?**

If the *top* was at the tail, then `push()` would work fine, but `pop()` would be disasterous!--requiring transversal
___

**LLL for Stacks**
+ Where do we add?
  - A `*tail` is not helpful 
  - The `*head` pointer *must* be **top**
  - There should be **no need to traverse**
+ If the size varies a lot, or cannot be allocated ***contiguously***, or is unknown
  - very small (~+3 operations) additional costs in run-time performance
  - ***does*** add the memory cost of **one additional address *per node***

```c++
int push(const datatype & argument)
	top = head;
	head = new node;
	head->data = toadd;
	head->next = temp;
	\\^(*head).next
```
___
**NOTE:**

By marrying arrays and link lists **(flexible array)**, we can avoind the run-time/memory problems between the two data types

___

***Flexible Arrays in Stacks***
+ In labs, *top* will be `top_index` (for array), with value of 0.
+ **PUSH**
  1. At `head = NULL`, store one item, and then `++top_index`
  2. If not empty: `top_index < SIZE`, store data at top and `++top`
  3. If array is full, `top_index == SIZE`, add new node at the beginning:
     - Code: `temp->next = head; head = temp; head = new node;`
+ **POP**
  1. *Empty* - return failure.
  2. If `top_index > 1`, you will `--top_index;` if dynamically allocated memory, `delete`
  3. If `top_index == 1`, decrement top (`--top`), `delete` dynamic memory as appropriate, and delete the first node (2nd node is now `head`)  
  4. If `head = NULL`, set `top_index == 0`

___
**NOTE:**

The preceding data structure will be used in both labs and in Program #2

___


Part 3
------
**Queues**
We can think of *stacks* as having only one end, since all ops are performed at the *top*. Hence it is called a **last in -- first out** data structure.
***Queues***, on the other hand, have two ends: A *front* and a *rear* (a **first in -- first out** structure)

*Que *Operations**
+ Adding to the *rear* of the que is to ***enqueue*** data
+ Removing from the *front* of the queue is to ***dequeue*** data
+ Can also ***peek*** at the *front*
+ A **DEQUE** is **not an operation**, it is a double-ended que
   - *enqueue* and *dequeque* at either end with **DEQUE**

**Client Interface**
+ How to implement is a decision of the programmer
  - should "is empty" be combinged with "dequeue"?
  - should "is full" be combinged with "enqueue"?
  - should dequeque return *and* remove the item at the front of the queue
  - should dequeue just return the item at the front, requiring also "peek"?

```c++
class queue {
	public:
		queue();
		~queue();
		int enqueue(const datatype & arg_name);
		int dequeue(datatype & arg_name);
		int peek(datatype & arg_name);
		int isempty(); int isfull();
		int dequeque(); 	\\if removing without arguments (unlikely) 
}
```
***Using Arrays with Queues***
*Problem* of **rightward drift** with *linear arrays*
```c++
enqueue(10);
\\[10]
\\front/rear
enqueque(20);
\\[10][20]
\\front  rear
enqueue(30);
\\[10][20][30]
\\front     rear
dequeue()
\\[ ][20][30]
\\   front rear
enqueue(50);
\\[ ][20][30][50]
\\   front     rear
```
**Do not** use linear arrays for queues,

Use **Circular Arrays**
+ Alter how indices are incremented
+ To increment index: `++index %= SIZE; array[index];`
  - 'new' *compound* operator  `%=`
  - the new index should be between 0 and (SIZE-1)

***Using LLL with Queues***
+ Programmer needs to understand where to *enqueue*.
  - **Rear** must be at the `tail` pointer.
    * rear/tail are synnonymous

***Circular Linked Lists with Queues***
Data structure where the *last* node points to the *first*.
+ Pointer is not `head`, choose `qptr` or `pointer`
+ Case 1: Pointer will be NULL if the list is empty
+ Case 2: With **one item**, that item **points to itself**
+ Case 3: With *more items*, rear points to the front of the list.

```c++
\\case # 3

enqueue(datatype & arg_name)
{
	temp = ptr->next;
	ptr->next = new node;
	ptr = ptr->next;
	ptr->next = temp;
}

dequeue(dtattype & arg_name)
{
	temp = ptr->next->next;
 	delete ptr->next;
	ptr->next = temp;
}
```
___
**NOTE ON RUNTIME PERFORMANCE:**

The array is the less efficient choice in queues, as pointer arithmetic creates more overhead

___
