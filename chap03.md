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
    Is the pattern <pre>01</pre> different from the pattern <pre>10</pre>?
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
| 4 |	16 | 2<sup>4</sup>|

How many patterns with 5 bits? Make two copies of the 4-bit patterns (16 patterns per copy). Make the patterns unique by prefixing "0" to the first 16 patterns and "1" to the second 16. You now have 16×2 = 2<sup>5</sup> unique patterns. This demonstrates the following:

**Number of possible patterns with N bits  =  2<sup>N</sup>**

Memorize this fact. Better yet, make lists of patterns (as above) and play around until you understand. Do this now. This is an essential fact. If you allow yourself to get muddled on it, you will waste much time in this and future courses.

How many patterns can be formed with 10 bits? Use the formula:

2<sup>10</sup> = 1024
This number occurs often in computer science. 1024 bytes is called a kilobyte, abbreviated K and pronounced "Kay".

### Question
<details>
    <summary>
        In the past, some computers used 16 bits to form memory addresses. Assuming no special tricks (which such limited machines often used), how many bytes maximum could be held in main storage?
    </summary>
    64K bytes:     2<sup>16</sup> = 2<sup>(6 + 10)</sup> = 2<sup>6</sup> × 2<sup>10</sup> = 64K
</details>

## 3.6 More About Patterns
| Number of Bits |	Number of Patterns | Number of Patterns as power of two |
|------------|------------|---------|
| 1 |	2 |	2<sup>1</sup>|
| 2 |	4 |	2<sup>2</sup>|
| 3	| 8 |	2<sup>3</sup>|
| 4	| 16 |	2<sup>4</sup>|
| 5	| 32 |	2<sup>5</sup>|
| 6	| 64 |	2<sup>6</sup>|
| 7	| 128 |	2<sup>7</sup>|
| 8	| 256 |	2<sup>8</sup>|
| 9	| 512 |	2<sup>9</sup>|
|10	| 1024 |	2<sup>10</sup>|

Many calculations involving bit patterns use the following familiar fact of arithmetic. (Although the fact is familiar, confusion is even more familiar. Be sure you know this factoid.)

**    2<sup>(N+M)</sup>   =   2<sup>N</sup> × 2<sup>M<sup>    **

It is not too much work to extend the table, as shown at right. You can always make this table from scratch, but memorizing a few key values does not hurt.

The numbers of patterns that can be formed with 10 or more bits are usually expressed as multiples of 1024 (= 2<sup>10</sup>) or in "Megs" (= 2<sup>20</sup>). For example, how many patterns can be formed from 24 bits?

224   =   2<sup>4</sup> × 2<sup>20</sup>   =   16 Meg
The power of two (24) splits into a small part (2<sup>4</sup>) and a part that has a name (2<sup>20</sup> = Meg). This is a useful trick you can use to amaze your friends and impress employers.

Some audio cards use 12 bits to represent the sound level at an instant in time (12 bits per sample). How many signal levels are represented?

2<sup>12</sup> = 2<sup>2</sup> × 2<sup>10</sup> = 4K levels

### Question
<details>
    <summary>
        You wish to save a GIF image using either 6 bits per pixel or 8 bits per pixel. Saving the image with 8 bits per pixel takes somewhat more memory. Which should you choose?
    </summary>
    Unless memory is at a premium, use 8 bits per pixel. With 6 bits, the image could only have 26 = 64 colors; with 8 bits, it can have 28 = 256 colors, a considerable improvement.
</details>

## 3.7 - Pattern Names
Consider the following pattern:

0010100010101010
It is not easy to work with. It is convenient to break bit patterns into 4-bit groups (called nibbles) (Haha!  Get it?  Half of a byte is called a nibble):

0010 1000 1010 1100
There are 16 ( = 2<sup>4</sup> ) possible patterns in a nibble. Each pattern has a name, as seen in this table.

Hexadecimal Names 

| nibble	| pattern name |	nibble	| pattern name |
| 0000	| 0 | 1000 |	8 |
| 0001	| 1	| 1001 |	9 |
| 0010	| 2	| 1010 |	A |
| 0011	| 3	| 1011 |	B |
| 0100	| 4	| 1100 |	C |
| 0101	| 5	| 1101 |	D |
| 0110	| 6	| 1110 |	E |
| 0111	| 7	| 1111 |	F |

You might be tempted to call those 4-bit patterns "binary numbers". Resist that temptation. The bit patterns in computer main memory are used for very many purposes. Representing integers is just one of them. The fundamental concept is "bit patterns". Don't confuse this concept with one of its many uses: "representing numbers".

The above bit pattern can be written using the pattern names:

0010 1000 1010 1100 = 28AC
Bits are grouped into nibbles starting at the right. Then each nibble is named. This method of giving names to patterns is called ** hexadecimal**.

### Question
<details>
    <summary>
        Name the following patterns:
            <br>0001 0001    
            <br>0011 1001    
            <br>1011 1111    
            <br>0100 0110    
            <br>0000 0000
    </summary>
    <br><br>
    0001 0001     11 <br>
    0011 1001     39 <br>
    1011 1111     BF <br>
    0100 0110     46 <br>
    0000 0000     00 (be sure to show both zeros)
    
## 3.8 - More Hex Practice
If there are not enough bits at the left to form a complete group of four, add zero bits to the left, (but be sure that it is clear by context how many bits you are describing). For example:

```
1010000010000010     =  
1010 0000 1000 0010  =  A082
```
Another example:
```
10100110101111      =  
10 1001 1010 1111   =
0010 1001 1010 1111 = 29AF
```
Usually `0x` is placed at the front of a pattern name to show that it is a hexadecimal pattern name:

```
0x0010  =  0000 0000 0001 0000
0xFACE  =  1111 1010 1100 1110
```
This helps us distinguish between a binary pattern `11` and the hexadecimal pattern `11` (which would be binary `0001 0001`).

Adding zeros to the left of a pattern creates a new pattern. The new pattern has its own name. `0x0 = 0000` is a different pattern than `0x00 = 0000 0000`. Sadly, people are not consistent about this, and depending on context, both patterns might be called `0x0`.

Keep in mind that hexadecimal pattern names are used by humans for talking about bit patterns. Inside the computer there are only bits and their patterns. Hexadecimal is used in books and documents (outside the computer) to describe these bit patterns.

<details>
    <summary>
        Name the following patterns; include 0x in the name:<br>
0000 1010 0001 0001    <br>
0001 0010 1001 1010    <br>
1111 1010 1101 1110    <br>
0011 0110 1100 0000    <br>
0000 0000 0000 0000    <br>
    </summary>
    0x0A11 <br>
    0x129A <br>
    0xFADE <br>
    0x36C0 <br>
    0x0000 (be sure to show all zeros)
</details>
 ## 3.9 - Octal
Sometimes documentation describes bit patterns in groups of three. Three-bit groups are named using the first eight pattern names of hexadecimal. This method is called octal notation. A bit pattern can be named using hexadecimal names, octal names, or many other notations.

Octal Names:

group |	pattern name | group | pattern name
| 000 |	0 |	100 |	4 |
| 001 |	1 |	101 |	5 |
| 010 |	2 |	110 |	6 |
| 011 |	3 |	111 |	7 |

Sometimes documentation describes bit patterns in groups of three. Three-bit groups are 

```
01101010 = 01 101 010 =  152 (octal)
01101010 = 0110 1010  = 0x6A (hex)
```
Octal is awkward to use with 8-bit bytes. Bytes don't evenly split into octal pattern names. But you should know about it. Historically, some computer documentation used octal pattern names. Also, in several programming languages (C and Java among them) octal notation is indicated by a leading zero:
```
0152    (octal)    = 001 101 010 
0x152   (hex)      = 0001 0101 0010 
152     (decimal)  = 1001 1000 
```
When the number of bits is not a multiple of three it is conventional to add zero bits to the left, and then to name the pattern as usual. This happens frequently because computer memory is organized into 8-bit bytes, which do not divide evenly into groups of three.

Programmers have lost an unfortunate number of hours with buggy programs, only to discover a constant buried deep in the code that started with a "0" when it should not have.

### Question
<detail>
    <summary>
     111 010 001    <br>
100 011 010    <br>
011011110    <br>
11000000    <br>
    </summary>
    <br> 0721 <br>
    0432 <br>
    0336 <br>
    0300 
    </details>

## Key Terms and Concepts
* bit pattens
* binary
* octal
* hexadecimal
* number of patterns represented by N bits = 2<sup>N</sup>





