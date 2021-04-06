CS163 Topic 1 - ADTs - Abstract Data Types - *Week 1*
==========================================
	
Programing Paradigms/Methodologies
----------------------------------- 
+ Procedural Abstraction - breaking down into meaningful goals/functions (162, 163)
+ Modular Abstraction - separate files/teams (.cpp, .h, .o, extenal data) - (162, 163, 202)
+ Data abstraction - classes managing themselves; building data types (163 - topic 1 and all term)
  - reduce size and complexity of programs
+ Object Oriented Programming (202)

Data Structures *(goals for the term)*
---------------
+ Spend time talking about different data structures and algorithms to solve problems, and 
  how to measure the efficiency of the approaches taken
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

## Creating an ADT   (the *todo_list* example)

| Todo Item |
:--------:
| name |
|priority
|doneflag

**Todo *list (LLL)***
1. **Keep track** of the things I need to accomplish.
2. **Save** the item's name and priority, and if it's been completed.
3. Underlying data **could be either a *struct* or a *class***
	- *We will be starting with a struct in this example*

|**List of Items** |_|_|_| 
|------------|-------------|-------------|--------------------|
| *create* | *destroy* | *insert*  | *display_main* |
| *display_all* | *remove_match* | *find* | *is_complete?* | 
 
 Our job is to write code to manage the data structure, while another part of our "team" is writing the client / application.
 **Coding example from class:**
```
#include <iostream>
#include <cstring>
#include <cctype>

//Name and the purpose of the file
//Comments should focus in a .h file on what the client program
//is going to need to know:  HOW are they going to USE
//this software
//client program <= Application, test program
//
//This is the class that is a managing a list of todo items
//The client can add new items, display items by choice
//remove matching items, and indicate if an item is done, so it can
//be checked off. This is representing an Abstract Data Type (ADT)

struct todo
{
        char * name;
        int priority;
        bool done;

};

struct node
{
        todo item;      //only reason to make the item a pointer: 1.array of items,  2. share member
        node * link;
};                      //separating out the data from the thing manaing the data
                        //so there is no
                        //
class todo_list
{
        public:
                todo_list();
                ~todo_list();
                ____insert(const todo & to_add);  //take the info from the argument and make a
                                                        //copy and store it in my data struct
                                                        //reutrn1 if the insert was successful
                                                        //0 otherwaise (to_add data had no data in it)
                //const after: is a "constant member function" - it means the member function
                //doesn't modify the data members (even if passed by reference)
                int display_match(const int match_priority) const; //reurn 0 if there are no matches
                int display_all() const; //fail itf there are no items in the list
                int remove_match(int match_priority);
                int finished_item(char name_of_finished_item[]);
        private:
                node * head;
		node * tail;
};
