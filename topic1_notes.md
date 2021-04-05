---


---

<h1 id="cs163-topic-1---adts---abstract-data-types">CS163 Topic 1 - ADTs - Abstract Data Types</h1>
<h2 id="programing-paradigmsmethodologies">Programing Paradigms/Methodologies</h2>
<ul>
<li>Procedural Abstraction - breaking down into meaningful goals/functions (162, 163)</li>
<li>Modular Abstraction - separate files/teams (.cpp, .h, .o, extenal data) - (162, 163, 202)</li>
<li>Data abstraction - classes managing themselves; building data types (163 - topic 1 and all term)
<ul>
<li>reduce size and complexity of programs</li>
</ul>
</li>
<li>Object Oriented Programming (202)</li>
</ul>
<h2 id="data-structures">Data Structures</h2>
<ul>
<li>The goal for this term is to spend our time talking about different data structures,<br>
algorithms to solve problems, and how to measure the efficiency of the approaches taken</li>
<li>NOT about learning new C++ syntax this term</li>
<li>APPLICATION of C++ and linear linked lists to new Abstract Data Types</li>
</ul>
<h2 id="data-structures-vs-adt">Data Structures vs ADT</h2>
<ul>
<li>Data structures specify HOW WE STPRE THE DATA
<ul>
<li>array, linked list, etc</li>
</ul>
</li>
<li>an Abstract Data Type specifies how a new data type BEHAVES:</li>
<li>it includes the data and operations that the new data requires;<br>
the data being stored in a data structure</li>
</ul>
<p><strong>Examples of ADTs</strong></p>
<ul>
<li>int</li>
<li>list</li>
<li>stack</li>
<li>queue</li>
</ul>
<p><em><strong>We will be building ADTs all term!</strong></em></p>
<ul>
<li>Data abrstraction - process of building an abstract data type</li>
<li>Abstract Data Type - a new data types that we create
<ul>
<li>has memory (data structures)  and functions (behavior)</li>
</ul>
</li>
<li>Data structure - how we organize the memory we use, how it is stored</li>
<li>Client vs Client program ( see ADT-client vs ADT.png)
<ul>
<li>not building applications…</li>
<li>Test Bed
<ul>
<li>can code be tested</li>
<li>User vs Application (client)</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="using-classes-to-build-adts">Using CLASSES to build ADTs</h2>
<ul>
<li>We will use the C++ class construct to build ADTs</li>
<li>The data (represented by the data structure)</li>
<li>are placed in the PRIVATE SECTION</li>
<li>The operations (what the “client” or application can do) is in the<br>
public section (prototypes)</li>
<li>The user and client should not be aware of what data structure is being used</li>
<li>client program should not be aware there is a node or a next pointer<br>
for a linked list, or an index to an array – if and array is used</li>
<li>Plug and play</li>
<li>this allows an ADT to to “plug and play” different data structures<br>
to maximize efficiency w/o disrupting the client program</li>
</ul>
<p><em><strong>Locations:</strong></em></p>
<pre><code>			Private:
				- data members
				- output of data (if requested by function)
			Public (client):
				- error messages
				- input data
				- output data 
				- prompting
</code></pre>
<ul>
<li>For each data member, ask: COuld this be a local variable to a member function<br>
instead?</li>
<li>If the value of the variable does not need to persist from operation<br>
to operation, it should NOT be a data member</li>
</ul>
<h2 id="static-or-dynamic-allocated-memory">Static or Dynamic Allocated Memory?</h2>
<ul>
<li>
<p>main program is the ONLY placew you should use statically allocated arrays</p>
</li>
<li>
<p>all arrays muyst be dynamically allocated</p>
</li>
<li>
<p>ADT needs to be used by many types of applications. Not all applications/script<br>
can use static memory</p>
</li>
<li>
<p>Think about efficiency</p>
</li>
<li>
<p>do not prompt member functions</p>
</li>
<li>
<p>only traverse lists when absolutely necessary</p>
</li>
<li>
<p>use pass by reference to reduce the information being continually copied</p>
</li>
<li>
<p>wear “different hats”</p>
</li>
</ul>
<h2 id="recursion-in-lll">Recursion in LLL</h2>
<p><strong>Coding:</strong></p>
<p>Questions to ask yourself:</p>
<ol>
<li>Is the problem repetative?</li>
<li>Is part of the problem repetitive vs not?
<ul>
<li>For example, if we are removing the first node and<br>
counting the number of nodes left, I’d remove the first node<br>
and THEN call a recursive function. Break it apart!!</li>
<li>A wrapper function that does the NON repetative part</li>
<li>A recursive function that does the repetative part</li>
</ul>
</li>
</ol>
<p><em>(when we use classes, the public functions shpould not have NODE pointers<br>
as arguments. What this means that when we use a class, we will actually need to have<br>
a public “wrapper” function that kick starts the private recursive function with a node<br>
pointer as an argument)</em></p>
<p><em><strong>For the repetitive part:</strong></em></p>
<ol start="3">
<li>What is the simplest stopping condition (the base case)<br>
(eg., if head is NULL)
<ul>
<li>plan out: What to do?</li>
</ul>
</li>
<li>Is there another stopping condition(or base case)
<ul>
<li>plan out what to do</li>
</ul>
</li>
<li>Is there something that needs to be done in this invokation?<br>
(outputting? counting? summing?)
<ul>
<li>plan out what to do</li>
</ul>
</li>
<li>How do we get to the next smaller subproblem?<br>
<em>(recursive call, that needs to work with a smaller part of the data)</em><br>
<em>(like calling the function with head-&gt;next)</em>
<ul>
<li><strong>DON’T</strong> traverse</li>
<li><strong>DON’T</strong> drag a previous pointer. RARELY needed</li>
<li><strong>DON’T</strong> put a RETURN statement on your function call automatically</li>
</ul>
</li>
<li>Is there something that needs to be done AFTER the recursive call?
<ul>
<li>if yes, plan out what to do</li>
</ul>
</li>
<li>Make sure you return the correct information.</li>
</ol>

