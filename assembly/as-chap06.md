# Chapter 6 - Number Representation
Patterns of bits can represent many different things. Anything that can be represented with symbols of any kind can be represented with bit patterns. This chapter shows how bit patterns are used to represent integers.

## Chapter Topics:
* Numbers and representations of numbers.
* Positional representation of integers.
* Decimal representation.
* Binary representation.
* Converting representations.

### Question
<details>
    <summary>
      What is your favorite number?
    </summary>
    42.  The answer is <a href="https://en.wikipedia.org/wiki/42_(number)#The_Hitchhiker's_Guide_to_the_Galaxy">always 42</a>.
</details>

## 6.1 - What is a Number?
In ordinary English, the word "number" has (at least) two different meanings. One meaning is the concept, the other meaning is how the concept is represented. For example, think about "the number of eggs in an egg carton."  You know the number I mean. Now write it down on paper.

What you wrote is a representation of the number. Here is another representation:

`XII`

This may not be the representation you used for your number. Here is another representation for that same number:

`///// ///// //`

Perhaps you used this representation:

`12`

or this:

`twelve`

or this:

1100<sub>2</sub>

Are any of these different numbers?  No, but the question is vague.

To be precise you would say that `XII`, `///// ///// //`, and `12` are different ways to represent the same number.

There are many ways to represent that number. The number is always the same number. But a variety of ink marks (or pencil marks, or chalk smudges, or characters on a computer monitor) can represent it. In normal conversation and in writing "number" often means the representation of a number. For example, you might call `12` a "number". It would be tedious to call it "an instance of the representation of a particular number using Arabic digits with the decimal system." But that is what it is.

Computer Science is concerned with using patterns of bits to represent things. It is important to be clear about the difference between the thing and a representation of the thing. For example, an integer may be represented using a bit pattern in computer memory. (There are many different ways to do this.) The integer is conceptual. The bit pattern is only a representation of the concept.

### Question
<details>
    <summary>
      Is XII even or odd?
    </summary>
    Even. The representation does not change the properties the number (although it often makes it easier to determine those properties).
</details>

## 6.2 - Positional Notation

The decimal system is a positional notation for representing numbers. This means that the representation consists of a string of digits. The position of each digit in the string is significant. Think of each position as a numbered slot where a digit can go.

____<sub>4</sub> ____<sub>3</sub> ____<sub>2</sub> ____<sub>1</sub> ____<sub>0</sub>

Positional notation has many advantages. It is compact: "78" is shorter than "LXXIIX". Computation is easy. LXXIIX times XLIIV is hard to do using the Roman numeral system.

### Question
<details>
    <summary>
      Is XLMCIIV a legitimate Roman-system representation of an integer?
    </summary>
    Yuck!
</details>

## 6.3 - Decimal Notation
The Roman numeral above is not a correct representation of an integer. But it takes some inspection (and perhaps a quick Google search) to decide this. Decimal positional representation is clearly better.

You already know how decimal notation works (and probably would be happy to skip this topic but humor me).

324 means:  3 × 100  +  2 × 10  +  4 × 1 

which is:   3 × 10<sup>2</sup>  +  2 × 10<sup>1</sup> +  4 × 10<sup>0</sup>

Remember that:
B<sup>0</sup>   =  1,  no matter what number B is.

Here we come to an astounding fact!  The numbering system you're most familiar with is called *decimal* because it's based on powers of ten!  This is important, so make a note of it.

Rules for Positional Notation.
1. The base, `B`, is (usually) a positive integer.
2. There are `B` "digits" representing zero up to (B minus one).  In other words, the decimal system (base 10) uses the digits 0, 1, 2, 3, 4, 5, 6, 7, 8, and 9.
3. Positions correspond to integer powers of `B`, starting with power zero, and increasing right to left.
4. The digit placed at a position shows how many times that power of `B` is included in the number.

### Question
<details>
    <summary>
    Fill in the blanks with the appropriate power of 10:<br>
      7305 = 7 × 10<sup>___</sup>  +  3 × 10<sup>___</sup>  +  0 × 10<sup>___</sup>  +  5 × 10<sup>___</sup></pre>
    </summary>
       7305 = 7 ×  10<sup>3</sup>  +  3 × 10<sup>2</sup>  +  0 × 10<sup>1</sup>  +  5 ×  10<sup>0</sup></pre>
</details>

For base 10 representation (often called decimal representation), the rules of positional notation are:
1. The base is 10.
2. There are 10 digits: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 .
3. Positions correspond to integer powers of 10, starting with power 0 at the rightmost digit, and increasing right to left.
4. The digit placed at a position shows how many times that power of 10 is included in the number.

Any integer can serve as the base for a positional representation system. Five can serve as a base. (This is called "quinary" numbering, if you were curious.)

### Question
<details>
    <summary>
    Here are the rules for positional notation. Fill in the blanks to work with base five:<br>
    The base is _____.<br>
    There are "digits": ___, ___, ___, ___, ___<br>
    Positions correspond to integer powers of ____ starting with power ____ at the rightmost digit, and increasing right to left.<br>
  The digit placed at a position shows how many times that power of ____ included in the number.
    </summary>
    <br>The base is five.<br>
There are five "digits": 0,1, 2, 3, 4 .<br>
Positions correspond to integer powers of five, starting with power 0 at the rightmost digit, and increasing right to left.<br>
The digit placed at a position shows how many times that power of five is included in the number.<br>
</details>


## 6.4 - Base Five Notation
The number "five" in base five is represented by "10" That is:

1 × (five)<sup>1</sup> + 0 × (five)<sup>0</sup>

The base in any positional representation is written as "10" (assuming that the usual symbols 0, 1, ... are used). Here is a number represented in base five: 421. It means:

421 = 4 × five<sup>2</sup>  +  2 × five<sup>1</sup> + 1 × five<sup>0</sup>.

Phew!  That's confusing!  How do we distinguish between 421 representing the quantity "four hundred twenty-one" (as we're used to in base 10) or the quantity "one hundred eleven" (as it would in base 5)?  To avoid confusion, sometimes the base being used is placed as a subscript: 421<sub>5</sub> means that base 5 is being used.  421<sub>10</sub> means that base 10 is being used.


## 6.5 - Changing Representations
You may wish to change the representation of a number from base 5 notation into base 10 notation. Do this by symbol replacement. Change the base 5 symbols into the base 10 symbol equivalents. Then do the arithmetic in base 10.

421<sub>5</sub>	  =  	4 × five<sup>2</sup> + 2 × five<sup>1</sup> + 1 × five<sup>0</sup>

the number in base 10	  =  	4 × 5<sup>2</sup> + 2 × 5<sup>1</sup> + 1 × 5<sup>0</sup>

the number in base 10	  =  	4 × 25 + 2 × 5 + 1 × 1

the number in base 10	  =  	100 + 10 + 1 = 111

The above process is often called "converting a number from base 5 to base 10". But in fact, the number is not being converted, its representation is being converted. The characters "421 (base five)" and "111 (base ten)" represent the *same quantity.*

### Question
<details>
    <summary>
    Change the representation of 1025 from base five to base ten.
    </summary>
    1025<sub>5</sub>   =   1 × 5<sup>2</sup> + 0 × 5<sup>1</sup> + 2 × 5<sup>0</sup>   =   2510 + 210   =   2710<sub>10</sub>
</details>

## 6.6 - Base Seven

Here is another example: 326<sub>7</sub>. This means:

3 × seven<sup>2</sup> + 2 × seven<sup>1</sup> + 6 × seven<sup>0</sup>

To write the number in decimal, write the powers of seven in decimal and perform the arithmetic:

3 ×  7<sup>2</sup> + 2 × 7<sup>1</sup> + 6 × 7<sup>0</sup> =

3 × 49  + 2 × 7 + 6 × 1 =

147 + 14 + 6    =    167<sub>10</sub>

### Question
<details>
    <summary>
    What is 682<sub>7</sub> in base-10 notation?
    </summary>
    Haha!  Trick question!  Remember the rules of positional representation? 8 is not a valid digit for the base-7 numbering system.  The only valid digits for a base-7 system are 0-6. 
</details>

## 6.7 - Bit Patterns
Bit patterns like 10110110110 are sloppily called "binary numbers" even when they represent other things (such as characters or machine instructions).

But, of course, bit patterns can be used to represent numbers. Base two positional notation is used for this.

### Question
<details>
    <summary>
    Here are the rules for positional notation. Fill in the blanks to work with base two:<br>
    The base is _____.<br>
    There are "digits": ___, ___ <br>
    Positions correspond to integer powers of ____ starting with power ____ at the rightmost digit, and increasing right to left.<br>
  The digit placed at a position shows how many times that power of ____ included in the number.
    </summary>
    <br>The base is two.<br>
There are two "digits": 0,1 .<br>
Positions correspond to integer powers of two, starting with power 0 at the rightmost digit, and increasing right to left.<br>
The digit placed at a position shows how many times that power of two is included in the number.<br>
</details>

## 6.8 - Representing Numbers using Base Two
From the rules for positional notation there are two digits. Usually "0" and "1" are chosen, and usually the word bit is used. "Bit" is an abbreviation of "binary digit".

In this system the base, the quantity two is written "10", the first power of two plus zero times the zeroth power of two. Each place in a representation stands for a power of two. Often this is called the binary system. Here is an example:

1011	=	1 × 2<sup>3</sup>	+	0 × 2<sup>2</sup>	+	1 × 2<sup>1</sup>	+	1 × 2<sup>0</sup>
 	    =	1 × 8	+	0 × 4	+	1 × 2	+	1 × 1
 	    =	8	+	0	+	2	+	1
 	    =	11<sub>10<sub>
    
The first line above uses decimal notation for the base and its powers. The remaining lines use base ten arithmetic until finally the integer is expressed in base ten positional notation.


### Question
<details>
    <summary>
        What is 0110<sub>2</sub> (binary representation) in base ten?
    </summary>
    0110 = 0 × 2<sup>3</sup>  + 1 × 2<sup>2</sup> + 1 × 2<sup>1</sup> + 0 × 2<sup>0</sup><br>
     = 0 + 4 + 2 + 0<br>
    = 6<sub>10</sub>
</details>

## 6.9 - Powers of Two
While not strictly required as a computer science student, it's often VERY useful to memorize some of the powers of two.  Since computers are digital and thus based on 0s and 1's (bits), powers of 2 crop up in many places.  I recomend memorizing up through 2<sup>10</sup> for convenience.

| Power of 2	| 10 |	9 |	8 |	7 |	6 |	5 |	4 |	3 |	2 |	1 |	0 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Decimal |	1024 |	512 | 256 |	128 |  64 | 32 | 16 |	8 |	4 |	2 |	1 |









        
        
        
