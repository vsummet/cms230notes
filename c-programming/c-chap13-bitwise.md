# Chapter 13 - Bitwise Operators in C

The "bitwise operators" in C are operators that are designed to manipulate a binary pattern at the bit level.  That is, we think of the "+" operator (for example) of operating on two numerical values and the result is also a numerical value.  However, the bitwise operators change the bit pattern of the variables.  It is then up to the program to determine how to interpret the new bit pattern.

In this class, we'll be focussing on the following bitwise operators:
* `>>` - right shift (arithmetic or sign-extending)
* `>>>` - right sign (logical)
* `<<` - left shift
* `&` - bitwise and
* `|` - bitwise or
* `^` - bitwise negate

## 13.1 - Representing Bit Patterns
The first thing to know is that we can use an integer "container" to store a bit pattern in C without really caring about what **quantity** the bit pattern represents.  C (specifically, the `gcc` compiler) allows us to use different prefixes to specify a pattern when we don't really care to figure out the corresponding 2's complement pattern.

For example, the following 3 variables all store the same bit pattern internally.  Work out the values and representations if you need to to verify this fact.
```
int binary_pattern = 0b00001101;
int hex_pattern = 0x0D;
int numerical_value = 13;
```

You can also specify octal representations with a leading 0, but this is confusing and leads to hard to understand code, so we won't be covering it here.

There are also ways to print out bit patterns easily using `printf`.  For example, consider the following code which allows us to print the hex representation of an integer value.

```
int num = 32;
printf("int value: %d \t hex rep: %x \n", num, num);
```

Unfortunately, there is no print specifier which allows us to easily print binary representations.  You'll need to convert from hex to binary yourself or write your own function if you want that capability.

## 13.2 - Shift Operators
The operators `>>`, `>>>`, and `<<` shift, that is "push", a bit pattern right or left.  The operators need the bit pattern to be manipulated and the number of places to shift the value.  Thus, the usage is:

```
bit_pattern_var shift_operator num_places
```

This example shifts the bit pattern stored in `x` to the left by 2 places.
```
x << 2
```

Shift operators are like other mathematical operators in that they do not change the variable they operator on.  Instead, we must assign the new pattern to a variable:

```
int y = x << 2;
or
x = x << 2;
```

### 13.2.1 - Left Shift
The left shift is the easiest to understand.  In this case, the number of bits (specified by the 2nd operand) are removed from the left-most portion of the bit pattern and the same number of 0's are concatenated to the right side of the pattern.  

For example, consider the pattern `0b01000101` stored in a variable called `x`.  (We'll use 8 bits to demonstrate the concepts, but remember that integers actually contain 32 bits (usually)).  If we evaluate the expression `x << 3`, we remove the 3 bits on the leftmost side of the bit pattern, `010` in this example, and "shove" the rest of the bits to the left. This gives us the pattern `00101`.  We then concatenate the same number of 0's to the right end of the pattern, giving us the pattern `00101000`.  

This operator is relatively easy to remember, since the operator itself points the direction the bits move: `<<` points left which is how the bits shift.  If the operator points right, we have some slight differences to iron out.

### 13.2.2 - Right Shift (Logical)
The logical right shift, `>>>` operates just like the left shift describe above except that it shifts the bit pattern to the right and adds 0's to the left.

If we again use the bit pattern `0b01000101` and evaluate the expression `x >>> 3`, we end up with the pattern `00001000`.

### 13.2.3 - Right Shift (sign-extending or arithmatic)
The  `>>` operator shifts right as well, but it performs a **sign-extending shift**.  Remember that for integers in 2's complement format (which all modern computers use), negative numbers will have a 1 in the left-most bit position.  If we were to shift the number right, we could change the sign from a negative to a positive.  There are good reasons for wanting a negative number to remain negative, even if it is shifted.  Consider the following example (again, done in 8 bits for simplicity, but the same concept applies to 32 bit integers as well).

Assume `x` is the bit pattern `11111011`.  This represents the value -5 in 2's complement format (for 8 bits).  If we shift the pattern 1 place to the right and shift in 0's, we would have the bit pattern `01111101` (this would be a logical shift, as described in 13.2.2).  This value is not a negative number!  Now it represents the integer value 125.

However, a sign-extending shift would shift in a 1 if the leftmost bit was a 1 and 0 if it was a 0.  That is, it maintains the most signficant bit in the pattern.  The resulting bit pattern `11111101` is the equivalent of -3.

Summary (again, in 8 bits for simplicity): 
```
int x = 0b11111011;
printf("x: %d, x >> 1: %d\n", x, (x >> 1));    //prints x: -5, x >> 1: -3
printf("x: %d, x >>> 1: %d\n", x, (x >>> 1));  //prints x: -5, x >>> 1: 125
```

If the most significant bit is a 0, then 0's are added and the shift acts like the logical shift described previously.





