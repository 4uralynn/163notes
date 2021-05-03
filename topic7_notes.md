
Topic 7: Measuring the Efficiency of Algorithms
===============================================

**So far** efficiency of various data structures has been discussed in a subjective manner.
+ We can *measure* efficiency using mathematical formulations using the Big **O** notation
  - allows us to more easily compare and contrast run-time efficience between algorithms & data structures


#### Algorithm Efficiency

***Algorithm A requires a certain amount of time proportional to f(N)***
+ regardless of the implementation or computer, there is some amount of time that A requires to solve the problem of size *N*
+ Alorithm *A* is said to be oreder *f(N)*, which is denoted ast ***O**(f(N))*
+ *f(N)* is called the algorithm's growth-rate function
  - *Big* ***O*** *Notation*
    * If a problem requires a constant time that is independent of the problem's size *N*, then the time requirement is defined as: ***O**(1)* (Example: Direct access)
    * If a problem of size *N* requires time that is directionally proportational to *N*, the problem is ***O**(N)*
    * If the time requirement is directly proportational to N<sup>2</sup>, then problem is ***O**(N<sup>2</sup>)*, etc...
+ Analyzing:
   - keep in mind differences in efficiency
     * traverse
     * memory
   - Notice what happens as the list size grows:
     * unsorted array and pointer base implementation may require more time to retrieve the desired node
     * A *hash table* (topic 6) implementation will always require the same constant amount of time
+ With large problems, efficiency is worth considering

___
**NOTE:**

*Always* keep in mind trade-offs between execution time and memory requirements. Big ***O*** denotes execution time, and does not account for memory requirements or algorithm or abstraction limitations.

___


***Evaluate*** performance needs and 
+ consider how much memory an approach requires
+ evaluate strengths/weaknesses of algorithm 
  - Are certain cases not handled effectively?
+ If problem size is **small**, an easy-to-code algorithm will probably be more appropirate than the most efficient
+ One algorithm  might require different times to solve different problems that are of the same size
  - i.e. searching for an item that is first in a list *vs* the item being at the last location


___
**NOTES ON BIG *O* NOTATION:**

+ Ignore lorder order *terms* in an algorithm's growth rate
  - Example: ***O**(N<sup>3</sup> + 4* x *N<sup>2</sup> + 3* x *N)* is the same as ***O**(N<sup>3</sup>)*

+ Ignore a *constant* being multiplied to a high-order *term*
  - Example: ***O**(5* x *N<sup>3</sup>)* is the same as ***O**(N<sup>3</sup>)*
+ Not all experts agree with this approach
   - Experts don't *all* agree. May be situations where the constaints have significance.

___


**Analyzing *Best* and *Worst* Case Scenarios**   
+ Consider the max time that an algorithm can require to solve a problem of size *N* 
  - **Worst** case
  - Algorithm is ***O**(f(N))* in the worst case.
+ Consider **average** case analysis (not implemented in CS163)
  - attempts to determine the amount of time that an algorithm requires to solve problems of size *N*
  - Generally *more difficult* to figure out than worst case analysis.


#### Put Into Practice:


|    *Type*          |                         Add                       |                Remove               |        Search             |            Display (Retrieval)         |
|--------------------|---------------------------------------------------|-------------------------------------|---------------------------|----------------------------------------|
|  **Sorted Array**  | **Best case:** ***O**(1)* + Binary Search, - Shifting , - Memory **Wort case:** ***O**(N)* | **Best case:** ***O**(log<sub>2</sub>N)* + Binary Search, - Shifting ***O**(N)* | + Binary Search ***O**(log<sub>2</sub>N)* | + Direct Access  ***O**(N)*| 
| **Unsorted Array** | ***O**(1)* + Direct Access, + **NO** Shifting, - Memory   | **B:** ***O**(1)* - **Sequential** Search, - Shifting **W:** ***O**(N)* |  - **Sequential** Search **W:** ***O**(N)*  | - *Must* implement a sorting algorithm ***O**(N<sup>2</sup>)* |
|     Sorted LLL     | **B:** ***O**(1)* - Sequential Search, + No Shifting, + Flex w/ Mem **W:** ***O**(N)* | **B:** ***O**(1)* - **Seq** Srch, + **NO** Shft, + Stop any time **W:** ***O**(N)* | - **Seq** Srch ***O**(N)* |               + Supported ***O**(N)* |
|    Unsorted LLL    | ***O**(1)* + Dir Accss, + **NO** Shft, + Flexibility w/ Mem  | **B:** ***O**(1)*   - Seq Srch, + **NO** Shft, +Flex w/ mem  **W:** ***O**(N)* | **B:** ***O**(1)* - **Seq** Srch **W:** ***O**(N)* |	- *Must* implement a sorting algoritm ***O**(N<sup>2</sup>)*  |


___
**NOTE:**

You would want to identify the circumstances for best/worst case.

___


