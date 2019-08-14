# Chapter 8 - Binary Addition and Two's Complement

Digital computers use bit patterns to represent many types of data. Various operations can be performed on data. Computers perform operations on bit patterns. With a good representation scheme, bit patterns represent data and bit pattern manipulations represent operations on data.

An important example of this is the **Binary Addition Algorithm**, where two bit patterns representing two integers are manipulated to create a third pattern which represents the sum of the integers.

## Chapter Topics:
* Single-bit Binary Addition Table
* Binary Addition Algorithm
* Addition in Hexadecimal Representation
* Sign-magnitude Representation
* Two's complement Representation
* Overflow detection in unsigned binary
* Overflow detection in two's complement binary

Most processor chips implement the Binary Addition Algorithm in silicon as part of their arithmetic logic unit. In a course in digital electronics you would study the hardware details of its implementation. This chapter only discusses the fundamentals of the algorithm.

### Question
<details>
    <summary>
    Compute the following. Give the answer in binary notation.
<pre>
    0 + 0 = ?
    0 + 1 = ?
    1 + 0 = ?
    1 + 1 = ?</pre>
    </summary>
    In binary:
<pre>
    0 + 0 = 0
    0 + 1 = 1
    1 + 0 = 1
    1 + 1 = 10</pre>
</details>

## 8.1 - The Binary Addition Algorithm
The binary addition algorithm is a bit-pattern manipulation procedure that is built into the hardware of (nearly) all computers. All computer scientists and computer engineers know it.  Simply put, it's how we add 2 binary numbers/patterns.

![binary addition algorithm](./images/ch08-binaryaddition.gif)

Let us start by adding 1-bit integers. The operation is performed on three bits. Arrange the bits into a column. The bit at the top of the column is called the "carry into the column". The operation produces a two-bit result. The left bit of the result is called the "carry out of the column".

To add two 1-bit (representations of) integers: Count the number of ones in a column and write the result in binary. The right bit of the result is placed under the column of bits. The left bit is called the "carry out of the column". The table shows the outcomes with all possible operands.

### Question
<details>
    <summary>
        Perform the following additions:
<pre>
  1             0             1
  0             1             1
  1             0             0  
----          ----           ---
</pre>
    </summary>
    In binary:
<pre>
  1             0             1
  0             1             1
  1             0             0  
 ----          ---           ---
 10            01            10
</pre>
</details>

## 8.2 - N-bit Binary Addition Algorithm
Adding a column of bits is as easy as counting. It is also easy to do electronically. It's a beginning project in many digital logic courses.

Now let us look at the full, n-bit, binary addition algorithm. The algorithm takes two operands and produces one result. An operand is the data that an algorithm operates on.

To add two N-bit (representations of) integers: Proceed from right-to-left, column-by-column, until you reach the left-most column. For each column, perform 1-bit addition. Write the carry-out of each column above the column to its left. The bit is the left column's carry-in.

![4 bit binary addition](./images/ch08-binaryaddition2.gif)

The example above adds two 4-bit operands, `0110` and `0111`. The initial conditions are shown on the left. First, add up the bits in the right-most column. There is no carry-in to this column, so all you need to do is count the bits. The result is 1 with a carry of 0. Write the 1 as the result for the column, and put the carry above the next column. The picture shows this in blue. Continue right-to-left through the columns until all columns have been added. The carry-out of the right-most column should not go into the sum, but should be written to the right of the other carry bits.


### Question
<details>
    <summary>
        Confirm that this addition is correct. Convert the binary numbers to decimal.  Hopefully the decimal answers add up.
<pre>
  0110     =    _____ (base 10) 
+ 0111     =  + _____ (base 10)  
_______        ________
  1101     =    _____ (base 10) 
</pre>
    </summary>
<pre>
  6
+ 7
----
 13
</pre>
    Success!
</details>

## 8.3 - A Longer Example
Here is another example. Observe that the binary addition algorithm is the same algorithm you use with ordinary base ten addition, except now the base two addition table is used for each column.

<table>
<tr>
<td>
<pre style="text-align:right">         
  0110 1110
+ 0001 0111
 -----------         
</pre>
</td>
<td>
<pre style="text-align:right">
         0 
  0110 1110
+ 0001 0111
-----------
          1
</pre>
</td>
<td>
<pre style="text-align:right">
        10 
  0110 1110
+ 0001 0111
-----------
         01
</pre>
</td>
<td>
<pre style="text-align:right">
       110 
  0110 1110
+ 0001 0111
-----------
        101
</pre>
</td>

<td>
<pre style="text-align:right">
     1 110 
  0110 1110
+ 0001 0111
-----------
       0101
      
</pre>
</td>
</tr>

<tr>

<td>
<pre style="text-align:right">
    11 110 
  0110 1110
+ 0001 0111
-----------
     0 0101
</pre>
</td>

<td>
<pre style="text-align:right">
   111 110 
  0110 1110
+ 0001 0111
-----------
    00 0101
</pre>
</td>
<td>
<pre style="text-align:right">
  1111 110 
  0110 1110
+ 0001 0111
-----------
   000 0101
</pre>
</td>
<td>
<pre style="text-align:right">
  01111 110 
   0110 1110
 + 0001 0111
 -----------
   1000 0101
</pre>
</td>

<td>
&#160;
</td>
</tr>

<tr>
<td colspan="5">
<br />
The carry out of the left column in the final sum
can be discarded, in this case. <br />
But in general you
must be careful with it.  See the following pages.
<br />
<br />
</tr>

</table>

The carry out of the left column in the final sum can be discarded, in this case. But in general you must be careful with it. We'll talk more about this in a bit. 

Check the answer by converting to decimal representation and doing the addition in that base (the same numbers are being added, but now represented in a different way, so the sum is the same.)

 <pre> 
   01111 110
    0110 1110    =  110 (base 10)
  + 0001 0111    =   23 (base 10)
  -----------      -----
    1000 0101    =  133 (base 10)
</pre>

## 8.4 - Details, Details
Here are some details:

1. Usually the operands and the result have a fixed number of bits (usually 8, 16, 32, or 64). These are the sizes that processors use to represent integers. 
2. To keep the result the same size as the operands, you may have to include zero bits in some of the leftmost columns. 
3. Compute the carry-out of the leftmost column, but don't write it as part of the answer (because there is no room if you have a fixed number of bits.)
4. When the operands are represented using the **unsigned binary** scheme (the base two representation scheme discussed in the last two chapters) a carry-out of  1  from the leftmost column means the sum does not fit into the fixed number of bits. This is called **overflow**.
5. When the operands are represented using the **two's complement** scheme (which will be described at the end of this chapter), then a carry-out of  1  from the leftmost column is not necessarily overflow.

Integers may be represented using a scheme called *unsigned binary* or using a scheme called *two's complement* binary. The binary addition algorithm is used with both schemes, but to interpret the result you need to know what scheme is being used. Overflow is detected in different ways with each scheme (see details 4 and 5, above.)

### Question
<details>
    <summary>
        The ARM chip has 32-bit registers. What do you think is the usual size of the operands when binary addition is performed?
    </summary>
        32 bits
</details>

## 8.5 - Overflow Detection
Here is an addition problem using 4-bit operands:

<pre>
 1111
  0111
+ 1001
------
  0000
</pre>
 
Overflow happened!

Two four-bit numbers are added, but the sum does not fit in four bits. If we were using five bits the sum would be `1 0000`. But with four bits there is no room for the left-most "1". Because the carry out from the most significant column of the sum is "1", the 4-bit result is not valid. The column is called the **most significant** column because it corresponds to the highest power of two. The bits in the leftmost columns are called the **most significant bits** or the **high-order bits**.

The electronic circuits of a processor can easily detect overflow of unsigned binary addition by checking if the carry-out of the leftmost column is a zero or a one. A program might branch to an error handling routine when overflow is detected.

### Question
<details>
    <summary>
        Add these unsigned numbers, represented in eight bits. Determine if overflow occurs.
<pre>
   0010 1100
 + 0101 0101
 -----------
 </pre>
    </summary>
    <pre>
        0 1111 100
          0010 1100
        + 0101 0101
        -----------  
          1000 0001
</pre>  
No overflow.
</details>
