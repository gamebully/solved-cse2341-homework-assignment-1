Download Link: https://assignmentchef.com/product/solved-cse2341-homework-assignment-1
<br>
<em>Submission Directions</em>:  Complete the questions below.  For questions that require diagrams, create the diagrams on your computer (no hand-drawn/scanned diagrams) using something like PowerPoint, Google Draw, or similar.  Copy-and-paste the diagrams into the correct place in the document you submit. For any code or pseudocode, use a fixed-point font (courier for example). Please submit a <strong><em><u>PDF</u></em></strong> file of your solutions.




<ol>

 <li>A stack overflow error means that more “data” has been placed on the stack than it can hold based on its size. Implement a simple recursive function that does not contain a base case.  How many times can this function call itself before you reach a stack overflow?  To answer this question, provide the count as well as the code for the recursive function.  Copy and paste the code for the recursive function in your solutions document. [10]</li>

</ol>




Answer:

count reached 261932 before segfault.




#include &lt;iostream&gt;




void overflow(int&amp; count){  std::cout &lt;&lt; count &lt;&lt; std::endl;  overflow(++count);

}




int main(){

int count = 0;  overflow(count);

}










<ol start="2">

 <li>Given:</li>

</ol>

char data[6][10]   = {“Sam”, “Robert”, “Mark”, “Jason”, “Alex”, “Karen”};

Determine the output of the following statements.  Note that some may print memory addresses.  If so, indicate the memory address by referring to the letter or array that it points to.  For example:

cout &lt;&lt; &amp;data[1][1];  a correct answer would be “address of o of Robert”.  If the statement contains an error, state such.

[2 points each]

<ol>

 <li>cout &lt;&lt; data[3];</li>

</ol>

Jason




<ol>

 <li>cout &lt;&lt; *data[2];</li>

</ol>

M




<ol>

 <li>cout &lt;&lt; *(*(data+1)+1);</li>

</ol>

o




<ol>

 <li>cout &lt;&lt; ***data;</li>

</ol>

Error, cannot dereference a char.




<ol>

 <li>cout &lt;&lt; **(data+ 4);</li>

</ol>

A




<ol>

 <li>cout &lt;&lt; *(data + 3);</li>

</ol>

Jason




<ol>

 <li>cout &lt;&lt; data;</li>

</ol>

The address of Sam







<ol start="3">

 <li>Draw the state of memory (a memory diagram) for the following code at the point indicated.</li>

</ol>




[10]







void foo(int *&amp; ptr)

{

int * x = new int[5];            ptr = x + 2;            //Draw memory diagram

//based on state of memory

//here

}










int main (){

int *p = new int[3];             p[0] = p[1] = p[2] = 5;

*p = 3;    *(p+1) = 6;            int * temp = p;     foo(p);   return 0;

}







Memory Diagram:







<ol start="4">

 <li>Draw the state of memory (a memory diagram) for the following code at the point indicated. [10]</li>

</ol>




int foo(int* p, int x)

{

for (int i = 1; i &lt;= 4; i++)

{

*(p) = *(p – 1) + x;

p++;

}

/*Draw memory diagram at this point*/

}




int main()

{




int z = 5;   int* m;

m = new int[z];   m[0] = 4;   z = 3;   foo(m+1, z);

return 0;

}

Memory Diagram:




<ol start="5">

 <li>What’s wrong with the code below? Feel free to compile and run the program to investigate. [6]</li>

</ol>




<table width="519">

 <tbody>

  <tr>

   <td width="342">#include &lt;iostream&gt; using namespace std; class HW1{public:    char *word; HW1() { }~HW1(){delete [] word;}};</td>

   <td width="177"> void foo(HW1 a){//some operation here} int main(){HW1 a;a.word = new char[80];strcpy(a.word, “abc”);foo(a);return 0;}</td>

  </tr>

 </tbody>

</table>




Answer:




Assuming the problem isn’t a missing #include &lt;cstring&gt; and that’s meant to be in the code, the problem is that there isn’t a copy constructor defined for HW1. When a is passed by value to foo, a shallow copy of it is made. That shallow copy then has the destructor called on it upon exiting the scope of foo, which calls delete[] on a copy of a.word. When the program exits main, the destructor is called on a, which calls delete[] on a.word. However, the memory that a.word points to has already been freed by the earlier delete[], causing a double free error.


