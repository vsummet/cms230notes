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
