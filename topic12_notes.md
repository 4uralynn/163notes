Topic 12: Sorting Algorithms
============================

Iterative Sorting
-----------------

Insertion sort will begin at the start of array or list and sort the rest of the data according to that data and any other data that has been sorted.
+ doubly nested loop
+ possibility of going through data *O*<sub>N<sup>2<\sup><\sub> for arrays
+ with doubly linked list, data is only compared once, and don't need to shift data (move once)

Selection sort will iterate and compare all data, and select the appropriate data to sort
* double nested loop
+ Going through data *O*<sub>N<sup>2<\sup><\sub> **all the time**
+ Only use if very costly to move data, and if doubly-linked list cannot be an alternative.

Exchange or "Bubble" sort will swap or bubble up the appropriate selections as iterating through the list.
+ High probability of making far more moves than necessary. 
+ Again a doubly nested loop for arrays.

Shell Sort will use the insertion sort on intervals of data, rather than the entire array
+ Possibly most powerful iterative alrogrithm

Radix sort will sort data into 'buckets' according to value.
+ **zero** compares
+ Lots of copying per bucket
+ *O*<sub> *keylength* (N) <\sub>


Recursive Sorting
-----------------

1. Mergesort
  + Recursive call to divide list in half
  + Merge sorted halves into one data structure
  + although extremely efficient run time, memory is used in temporary data structure
    - if temporary data structure isn't used, then it really isn't any better
    - with liked list, huge difference in efficiency between mergesort and insertion
2. Quicksort
 + "Divide and conquer" sorting algorith
 + partitions list of data items that are less than a pivot point and those greater or equal
 + Recursive steps
   1. Choose a pivot point from the list - very important choice
   2. Partition elements around the pivot
   3. Swap pivot value with rightmost in left partition
