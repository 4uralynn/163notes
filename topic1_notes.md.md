CS163 Topic 1 - ADTs - Abstract Data Types
==========================================
	
Programing Paradigms/Methodologies
----------------------------------- 
+ Procedural Abstraction - breaking down into meaningful goals/functions (162, 163)
+ Modular Abstraction - separate files/teams (.cpp, .h, .o, extenal data) - (162, 163, 202)
+ Data abstraction - classes managing themselves; building data types (163 - topic 1 and all term)
  - reduce size and complexity of programs
+ Object Oriented Programming (202)

Data Structures
---------------
+ The goal for this term is to spend our time talking about different data structures,
  algorithms to solve problems, and how to measure the efficiency of the approaches taken
+ NOT about learning new C++ syntax this term
+ APPLICATION of C++ and linear linked lists to new Abstract Data Types

		
Data Structures vs ADT
----------------------
+ Data structures specify HOW WE STPRE THE DATA
  - array, linked list, etc
+ an Abstract Data Type specifies how a new data type BEHAVES:
+ it includes the data and operations that the new data requires;
  the data being stored in a data structure

**Examples of ADTs**
+ int
+ list
+ stack
+ queue
		
***We will be building ADTs all term!***

+ Data abrstraction - process of building an abstract data type
+ Abstract Data Type - a new data types that we create
  - has memory (data structures)  and functions (behavior)
+ Data structure - how we organize the memory we use, how it is stored
+ Client vs Client program ( see ADT-client vs ADT.png)
  - not building applications...
  - Test Bed
    * can code be tested
    * User vs Application (client)

Using CLASSES to build ADTs
---------------------------
+ We will use the C++ class construct to build ADTs
+ The data (represented by the data structure)
+ are placed in the PRIVATE SECTION
+ The operations (what the "client" or application can do) is in the
  public section (prototypes)
+ The user and client should not be aware of what data structure is being used
+ client program should not be aware there is a node or a next pointer
  for a linked list, or an index to an array -- if and array is used
+ Plug and play
+ this allows an ADT to to "plug and play" different data structures
  to maximize efficiency w/o disrupting the client program

***Locations:***
```
			Private:
				- data members
				- output of data (if requested by function)
			Public (client):
				- error messages
				- input data
				- output data 
				- prompting
```
+ For each data member, ask: COuld this be a local variable to a member function
  instead?
+ If the value of the variable does not need to persist from operation
  to operation, it should NOT be a data member

Static or Dynamic Allocated Memory?
-----------------------------------
+ main program is the ONLY placew you should use statically allocated arrays
+ all arrays muyst be dynamically allocated
+ ADT needs to be used by many types of applications. Not all applications/script
  can use static memory

+ Think about efficiency
+ do not prompt member functions
+ only traverse lists when absolutely necessary
+ use pass by reference to reduce the information being continually copied
+ wear "different hats"
	

## Recursion in LLL

**Coding:**

Questions to ask yourself:

1. Is the problem repetative?
2. Is part of the problem repetitive vs not?
   - For example, if we are removing the first node and
     counting the number of nodes left, I'd remove the first node
     and THEN call a recursive function. Break it apart!!
   - A wrapper function that does the NON repetative part
   - A recursive function that does the repetative part
		
 *(when we use classes, the public functions shpould not have NODE pointers
  as arguments. What this means that when we use a class, we will actually need to have
  a public "wrapper" function that kick starts the private recursive function with a node
  pointer as an argument)*

***For the repetitive part:***
		
3. What is the simplest stopping condition (the base case)
   (eg., if head is NULL)
   - plan out: What to do?
4. Is there another stopping condition(or base case)
   - plan out what to do
5. Is there something that needs to be done in this invokation?
   (outputting? counting? summing?)
   - plan out what to do
6. How do we get to the next smaller subproblem?
   *(recursive call, that needs to work with a smaller part of the data)*
   *(like calling the function with head->next)*
   - **DON'T** traverse
   - **DON'T** drag a previous pointer. RARELY needed
   - **DON'T** put a RETURN statement on your function call automatically
7. Is there something that needs to be done AFTER the recursive call?
   - if yes, plan out what to do
8. Make sure you return the correct information.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4MTc4NjUzNF19
-->