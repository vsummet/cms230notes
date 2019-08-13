# Chapter 7 - Binary and Hex Integer Representation

Base 16 is often used to represent integers. Integers represented in base 16 are said to be represented with hexadecimal notation. The hexadecimal representation of an integer is equivalent to the pattern name of the bits in the binary representation of the integer.

It is easy to convert the representation of an integer between binary and hexadecimal. Converting representations between decimal and an arbitrary base is somewhat more difficult. The chapter presents some algorithms for doing this.

Chapter Topics:
* Left and right shifts
* Unsigned binary representation
* Familiar binary integers
* Hexadecimal representation
* Equivalence of hexadecimal representation and bit pattern names
* Converting representations from hexadecimal to binary
* Converting representations from decimal to any base

## 7.1 - Left Shift
Useful Fact: If the number N is represented by a bit pattern X, then X0 represents 2*N.

If 00110010<sub>2</sub> represents 50<sub>10</sub> , then 00110010**0** represents 100<sub>10</sub>. 

This is called "shifting left" by one bit. It is often used in hardware to multiply by two. Often you need the "shifted" pattern to have the same number of bits as the original pattern. Doing this with eight bits, 01100100 represents 100<sub>10</sub> (notice that we removed the leftmost 0 of the pattern).  If you must keep the same number of bits (as is usually true for computer hardware) then make sure that no "1" bits are lost on the left.

### Question
<details>
    <summary>
      With 8 bits, there are 2<sup>8</sup> patterns. What is the largest positive integer that can be represented in 8 bits using base two?
    </summary>
    2<sup>8</sup> - 1  =  256 - 1  =  255.<br> 
  There are 256 patterns possible with 8 bits. But when these patterns represent integers, One of the patterns (0000 0000) is used for zero.  You could also figure this out by noting that 11111111<sub>2</sub> is 255.
</details>

## 7.2 - Largest Positive Integer in N Bits
The representation scheme we are looking at is called unsigned binary because no negative numbers are represented. Often when people say "binary number" this is what they mean. Here are some of its characteristics:

1. With N bits, the integers 0, 1, 2, ... , 2<sup>N</sup> - 1 can be represented.
So, for instance, with 8 bits, the integers 0, 1, ..., 2<sup>8</sup> - 1 can be represented. These are the values 0 ... 255.

2. With N bits, zero is represented by 0....0....0 (all 0's).

3. (2<sup>N</sup> - 1) is represented by 1....1....1 (all 1's).

These facts are NOT always true for other representation schemes! Know what scheme is being used before you decide what a pattern represents.


### Question
<details>
    <summary>
Without doing any calculation, which of the following is the decimal equivalent of 1111 1111 1111?<br>
A. 2048<br>
B. 4095<br>
C. 16384<br>
D. 18432<br>
Look at fact 3 in the list and think a bit.<br>
<br>
Hint: Actually, you should think about a bit.<br>
    </summary>
4095<br><br>

A clever trick: perhaps you realized that the represented number is 2<sup>N</sup> - 1 which must be an odd number. ( 2<sup>N</sup> means 2 × 2 × 2 ... × 2 it must be even. So 2<sup>N</sup> - 1 must be odd. )<br><br>
So you picked the only odd number in the list. Or else you ignored the question.
</details>

## 7.3 - Base 16 Representation
Recall the Rules for Positional Notation:

1. The base B is (usually) a positive integer. 
2. There are B "digits" representing zero up to (B minus one). 
3. Positions correspond to integer powers of B, starting with power zero, and increasing right to left. 
4. The digit placed at a position shows how many times that power of B is included in the number. 

Rule 1 says any positive integer can be used as a base. Let's use sixteen as a base. Rule 2 says we need sixteen symbols to use as digits. The usual choices are the digits 0-9 and the letters A-F.
| Decimal | Hex Digit |
|----------|----------|
| 0 | 0 | 
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | A |
| 11 | B |
| 12 | C |
| 13 | D |
| 14 | E |
| 15 | F |

Since there are only ten of the usual digits, letters are used for the remaining six hex "digits".

Base sixteen representation is called the **hexadecimal system**, or just **hex** for short.

