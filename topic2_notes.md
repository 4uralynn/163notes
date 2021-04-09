Topic 2: Creating ADT  - Part 1
==============================

### Review:
***Data Abstraction*** process of creating a new data type
*Step-by-step using*
+ classes
+ constructors
+ member functions
+ data hiding
+ distinguishing the difference between what the *client* can do and that the ADT can do

List Abstraction
----------------

Building a "list" abstraction
+ *Remember* the data structure used should be able to 'plug and play' (i.e. be replaced without effecting the client program.)
+ Operations will include:
  - insert, remove, retrieve, and display
  - create, destroy

*Once the operations are understood,* we can
+ data will include the student name, current grade percent in the class, and PSU ID#
+ we can use a struct or a class
+ this topic examines both

The list can be implemented using a variety of data structures:
+ array (usually dyanamically allocated *only* for an ADT)
+ linear linked list
+ *circular* linked list **[*NEW* concept]**
+ *doubly* linked list **[*NEW* concept]**

```
struct student {
	char * name;
	char * psu_id;
	float grade;
};
```
**Options for placement of stuct:**
Before the class in the header file *(recommended)*
```
struct student {
	//data members
};

class list {
	public:
		//...
```

*Allows interaction of the client and member function.*
Non-node data members should be **objects** not **pointers** in (CS163) unless an array (dynamically allocated) or sharing memory) 

In the implementation *(hidden; used in C)*

*In* `.h` *file, create an 'incomplete declaration'*

```
struct student;
class list {
	public:
		//...
//... later, in .cpp file...

struct student {
	char * name;
	char * psu_id;
	float grade;
};
```
*This is mostly done in the C programming language*


Nested within class *(old school and not reccommended)*

```
class list {
	public:
		//member functions
	private:
		struct student {
			char * name;
			char * psu_id;
			float grade;
		};
};
```
*Avoid nesting as it is the reason for `namespace` (will discuss in CS202)*

**Struct vs Class**
If a class has been used, the members would have been private by default, requiring the list class to be declared as a frien

```
class student {
 	//public members
	private:
		char *name;
		friend class list;
};
```
*Do not do in this class*

Defining the List Class
-----------------------
*Conventions*
+ list public section first
   - client programmer can find member functions to call easily
+ last private section afterwards
   - in Java, member functions are implemented in the the class, so data goes first in Java
+ alywas provide default constructor 
   - initialize data members
+ always profide default destructor when deallocating dynamic memory
+ in this class, other function names will be provided, but *you* must create arguments
+ ***NEVER*** pass a `stuct` by value.
+ The `const` keyword in the argument prevents the client from changing memory of the argument passed by reference (only copy from)
   - `int insert(const student &)`
+ Ouside the argument, `const` means the member function can copy, but not change the private data members of the class
   - `int display() const;`
+ return member functions as `int` or `bool`
+ **Public functions** should not use a get_head function!!!
+ cannot return `struct`, *always* pass `struct` by reference

***Example of class interfacei (with typical member functions):***
```
class list {
	public:
		list();
		~list();
		int insert(const student &);
		int retrieve(char * input, student &);
		int display();
		int remove (char * input);
//...
```
#### Comments ####
*Perfect* your comments

|                  .cpp                    |                           .h                             |                       .cpp                        |
|------------------------------------------|----------------------------------------------------------|---------------------------------------------------|
|   Main / Application / Test Program      |     Class Interface                                      |           Implementation of Member Functions      |
|   ***Comments:***                        |       ***Comments:***                                    |                    ***Comments:***                |
| *How does it fully meet the test plan?*  | *Why you would want to use the data type?*               |                    *Algorithm*                    |
|                                          |  *How to call the functions: *arguments, data returned*  |   *How you are working with the data structure*   |
|                                          | *Aimed at application programmer*                        |  *Aimed at a programmer maintaining the software* |









### Exception Handling - [(link)][1]
Not something we will be doing in CS163
+ Will be tackled later in CS202
+ Can choose to work with it, but not required or officially part of the course
+ Not necessary in C++, but is in Java.
+ When there is an exception in your code

### How many classes, how many structs.
1. Structs or classes may be used for underlying data
2. The client should have no knowledge of the data structure.

[1]: https://www.cs.pdx.edu/~karlaf "Karla Fant's PSU Website"


