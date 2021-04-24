Topic 5: Other Linked Lists
===========================
Part 1
------

**Learning Goals:**
+ algoriths to manage circular and doubly linked lists
+ Dummy head nodes: Advantages and disadvantages
+ arrays of linked lists, or linked lists of arrays
+ Benefits/Drawback considerations of doubly "threaded" list

***Dynamic*** **Linked Lists**
Wisely controlled dynamic memory can save *considerable* memory that may be wasted by other implementations.
+ Not limited to fixed size restrictions
+ Certain operations are simpler with linked structures
  - no shifting once we have found the location
+ algoritms may be more complex, harder to read, and harder to debug than similar algorithms with statically allocated structures
+ Think Program 1: How would an array have changed the debugging process?
  - Same functionality or is some missing?
+ Can sometimes **waste** memory
  - can store many pointers, but maybe have little data
  - pointer space must be considered as overhead, which is accentuated when nodes contain a small amount of data
  - Allocating and deallocating memory at run-time is overhead and can overshadow the time saved by simple list-processing algorithms

>
> No hard or fast rules!
>                           - Karla
>
These are not just *coding* exercises in CS163. It is about decision - making.

***Doubly Linked Lists***
These avoid the need to manage a current/previous pointer when traversing!
+ Great for when you are consistantly going forwards and backwards through the list.
+ Two linking pointers, so is ***double*** the memory.
  - Have to weigh the advantages vs disadvantages per program
  - If the only advangage is not dragging a current pointer, then probably not worth it

**For a** ***LLL***
```c++
if (target)
	target->next = current->next;
else head = current->next;
```

**For a** ***DLL***
```c++
if (current->prev) {
	current->prev->next = current->next;
}
else head = current->next;
if (current->next)
	current->next->prev = current->prev;
```

**For a** ***Circular Linked List***
+ Traversing would be different
  - No beginning. No end.
+ No `NULL` check while traversing (just if the list is empty)

#### Dummy Head Nodes ####
*Variations* to singly linked lists have been *designed to decrease the complexity* and **increase the efficiency** of specific algorithms
+ For many algorithms, the first node is a *special case*
  - updating a head pointer is different than a next pointer of another node
  - consider inserting or deleting at head
+ Head is no longer a pointer. It is a node.
+ May *slightly* lessen the code you have to write, since head will never be a `NULL` case.
  - Doesn't seem to be worth it in the long run, but industy may use the concept.
