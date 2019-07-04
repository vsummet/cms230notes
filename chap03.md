# Chapter 3 - Bits and Bit Patterns

Computers represent data and instructions with patterns of bits. You must become familiar with bit patterns! This chapter will help you. It discusses the fundamentals of bit patterns.

Chapter Topics:
* Patterns of bits.
* The number of patterns that can be formed for N bits.
* How to systematically list all the patterns for N bits.
* Multiplying powers of two.
* Bytes, kilobytes, megabytes, and gigabytes.
* Names for four-bit patterns.
* Hexadecimal names for bit patterns.
* Octal names for bit patterns.

Remember that 8 contiguous bits are called a byte. A bit holds a zero or a one, possibly representing the on/off condition of a switch or transistor.

### Question
<details>
<summary>
How many patterns can be formed with a single bit? (Hint: click on the arrow!)
</summary>
2.  "0" is one pattern and "1" is the other. (Or "off" and "on".  Or "true" and "false".)
</details>
## 3.2 - Patterns of Bits
A bit can be 0 or 1. With one bit there are two possible patterns. How many patterns can be formed with two bits? Here is a complete list:
```
    0 0
    0 1
    1 0
    1 1
```
Looks like 4 patterns.

### Question
<details>
<summary>
Is the pattern `01` different from the pattern `10`?
</summary>
Yes.  The order (or position) of the bits matters.
</details>

## 3.2 -  How Many Patterns with Three Bits?
How many patterns can be formed with three bits? Let's list them:
```
    0 0 0
    0 0 1
    0 1 0
    0 1 1
    1 0 0
    1 0 1
    1 1 0
    1 1 1
```
Looks like 8 patterns.

### Question
<details>
<summary>
Is the number of patterns that can be formed with N bits greater than the number of bits?
</summary>
Yes ― much greater. This simple fact is of profound importance to computer science.
</details>

## 3.3 - Listing Patterns Systematically
There is a standard method for listing all of the patterns that can be formed with a given number of bits. First, list all of the patterns that can be formed with one bit:
```
0
1
```
To increase the number of bits (from one to two) make two copies of the list:
```
0
1

0
1
```
Within each copy, each row is unique. Now, make each row in the combined list unique. Do this by putting a "0" in front of each line of the first copy, and a "1" in front of each line of the second copy:
```
0 0
0 1

1 0
1 1
```
Now each line is unique and you have a complete list of the possible patterns of two bits. The number of unique patterns with 2 bits is double that with 1 bit.

For additional bits, repeat the trick for each new bit.

### Question
<details>
<summary>
How many patterns can be formed from 3 bits?
</summary>
8 patterns can be formed from 3 bits.
</details>

## 3.4 - How Many Patterns from Three Bits?
Repeat the trick. Make two copies of the table for two bits:
```
  0 0
  0 1
  1 0
  1 1
  
  0 0
  0 1
  1 0
  1 1
```
Now make each row unique by putting a "0" in front of the first group and a "1" in front of the second group:
```
0 0 0
0 0 1
0 1 0
0 1 1
  
1 0 0
1 0 1
1 1 0
1 1 1
```
Now you have all the patterns that can be formed from three bits.

### Question
<details>
<summary>
How many patterns can be formed from N bits?
</summary>
Twice the number of patterns that can be formed from (N-1) bits.
</details>

## 3.5 - How Many Patterns from N Bits?
The list of patterns for three bits has 8 lines (patterns). To form the list of patterns for 4 bits, make two copies of the list for 8 bits. This gives you 16 lines. Each line is made unique by prefixing the first half with "0" and the second half with "1".

Of course, the trick can be repeated as many times as you like. Adding one more bit doubles the number of patterns. The table shows the number of patterns for 1, 2, 3 and 4 bits.

| Number of Bits |Number of Patterns |	Number of Patterns as power of two |
|----------------|---------------|------------------|
| 1 |	2 |	2<sup>1</sup>|
| 2 |	4 |	2<sup>2</sup>|
| 3 |	8	|2<sup>3</sup>|
| 4 |	16 | 2<sup>4</sup?|

How many patterns with 5 bits? Make two copies of the 4-bit patterns (16 patterns per copy). Make the patterns unique by prefixing "0" to the first 16 patterns and "1" to the second 16. You now have 16×2 = 2<sup>5</sup> unique patterns. This demonstrates the following:

Number of possible patterns of N bits  =  2N
Memorize this fact. Better yet, make lists of patterns (as above) and play around until you understand. Do this now. This is an essential fact. If you allow yourself to get muddled on it, you will waste much time in this and future courses.

How many patterns can be formed with 10 bits? Use the formula:

210 = 1024
This number occurs often in computer science. 1024 bytes is called a kilobyte, abbreviated K and pronounced "Kay".




