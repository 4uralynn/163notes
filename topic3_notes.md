Topic 3: Building Ordered Lists  - Part 1
=========================================

**Ordered List ADTs**
+ What are they?
+ Discuss two different interpretations of an "ordered list"
+ Are manipulated by "position"

**Use of data structures for ordered lists**
+ arrays (statically & dynamically allocated)
+  LLL

We sometimes assume lists are ordered. That is not something to assume, as not all lists are ordered. We can add **position-oriented abstractions** so the application sends us to the correct position in list.

### Ordered Lists Defined
An **ordered list ADT** is implemented using LLL, circular linked lists, linked list of linked lists, doubly linked lists, etc.

**Any list can be...**
+ ordered by time
+ in order of thought of *(ie. grocery lists)*
+ to-do lists *(in priority order)*

**An *ordered list* is**
+ ordered by *position*
+ whereas *sorted* ;ist is a *value-oriented list* -- this is a **position oriented list**

**Two Interpretations Discussed:**
+ absolute lists - not every blank needs to be filled in *(ie. forms, tax forms)* 
+ relative lists - data is grouped together - no gaps *(ie editors)*

*There are many interpretations to where the data is inserted, and whether or not the list has "holes".*

#### *Absolute* Ordered Lists - Array

| - | - | - | - |  -  |  X |  -  |     -    |
|---|---|---|---|-----|----|-----|----------|
| 0 | 2 | 3 | 4 | ... | 32 | ... | size - 1 |

Benefits from **direct access** - `array[32]` / `*(array + 32 )` is position 33, and you can go *directly* there.

**Memory Issues with arrays**
+ How much?
+ Possible waste
+ Can we allocate all that is needed *contiguously*?

#### *Relative* Ordered Lists - Arrays
Direct access is not as much of a benefit, since all the memory is grouped together.

**BIG ISSUES**
+ *SHIFTING* data. If you are not appending
   - If you need to add data to middle or beginning, then you will have to shift all data
   - Use LLL instead for relative list needs
+ Requires additional array of pointers

#### *Absolute* LLL
Benefits from memory not being *required* to be contiguous. No need to know how much memory is needed, and *no* waste for overestimating.

**BIG ISSUES**
+ There is one whole extra address per node - so **memory overhead** required
  - (10,000 nodes is 10,000 addresses)
+ **SEQUENTIAL SEARCH** is ***horrible***
  - There is no direct access to get directly to data
  - No good if there are holes in the data
+  Requires a *position* data member
+  Use an array for a absolute list needs

#### *Relative* LLL
Benefits from not needing to be aware of the number of items, and there is no need for memory to be contiguous. It avoids the shifting with a relative array. There is no need to store position numbers and should not.

The only **negative issue** with a relative linear linked list:
+ *Requires* traversal
  - not fun, but better than an array for relative lists

## The *Alternative* Absolute Ordered List

**The *Flexible* Array**
*A linear linked list with an array at each node.*
```
[ ]-> [ ]]-> [ ]]-> [ ]/]
       v      v      v
  array1[] array2[] array3[]
```

Coding Example:
```c++
struct node
{
	data * array;
	node * link;
};
```

To determine how far to traverse you can use `(data_position - 1) / array_size)`. 

And to tell which index in the array, use `(data_position - 1) % array_size`.
___
**EXAMPLE**

To understand the previous paragraph, imagine a flexible linked list with 3 nodes--like the one above--and each array has 1000 data spaces.

If you wanted to get to the 1,032<sup>nd</sup> data position, `(1032 - 1) / 1000` would return the value `1`. So we would traverse 1 node. 

Then, `(1032 - 1) % 1000` would reurn the value `30`, so we would go to index `30`, `array2[30]`.
___

## The *Alternative* Relative Ordered List

**The *Array of LLL***
```
[ ],[ ],[ ],[ ],[ ],[ ],[ ],[ ]
 v   v   v   v   v   v   v   v
ptr ptr ptr ptr ptr ptr ptr ptr

//Each pointer goes to a separate spot on a LLL or to a separate LLL
```


