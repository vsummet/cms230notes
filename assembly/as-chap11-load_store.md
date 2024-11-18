# Chapter 11 - Memory Access Instructions and Variables

## 11.1 - Loads and Stores
First remember what it means for the ARM to be a **load-store architecture**: The operands for all arithmetic (and logic) operations are contained in registers. To operate on data in main memory, the data is first copied into registers. A **load operation** copies data from main memory into a register. A **store operation** copies data from a register into main memory.

When a word (4 bytes) is loaded or stored the memory address must be a multiple of four. This is called an alignment restriction. Addresses that are a multiple of four are called **word aligned.** This restriction makes the hardware simpler and faster.

The `ldr` instruction loads a word into a register from memory. The `str` instruction stores a word from a register into memory. Each instruction specifies a register and a memory address.

## 11.2 - Big Endian and Little Endian
A load or store instruction uses only one memory address. The lowest address of the four bytes is used for the address of a block of four contiguous bytes.

How is a 32-bit pattern held in the four bytes of memory? There are 32 bits in the four bytes and 32 bits in the pattern, but a choice has to be made about which byte of memory gets what part of the pattern. There are two ways that computers commonly do this:

1. Big Endian Byte Order: The most significant byte (the "big end") of the data is placed at the byte with the lowest address. The rest of the data is placed in order in the next three bytes in memory.
2. Little Endian Byte Order: The least significant byte (the "little end") of the data is placed at the byte with the lowest address. The rest of the data is placed in order in the next three bytes in memory.

In these definitions, the data, a 32-bit pattern, is regarded as a 32-bit unsigned integer. The "most significant" byte is the one for the largest powers of two: 2<sup>31</sup>, ..., 2<sup>24</sup>. The "least significant" byte is the one for the smallest powers of two: 2<sup>7</sup>, ..., 2<sup>0</sup>.

For example, say that the 32-bit pattern `0x12345678` is stored at address `0x00400000`. The most significant byte is `0x12`; the least significant is `0x78`.  Here is a graphic showing this example and the two different approaches.

![images/ch11-bigLittleEndian.gif]

Important: Within a byte the order of the bits is the same for all computers (no matter how the bytes themselves are arranged).

Many modern processors (including the ARM) are **big-endian**.  That is, they can support data in both little- and big-Endian specifications.  However, ARM by default is little-Endian, and instructions are always stored in little-Endian format.


### Question
<details>
    <summary>
      Here is a bit pattern, with the most significant bits written on the left (as usual): 0xFF00AA11. Copy the bytes to memory addresses 0x4000 - 0x4004 using big endian and little endian orders.
    </summary>
    Little Endian stores FF at 4003, 00 at 4002, AA at 4001, and 11 at 4000.  Big endian stores 11 at 4003, AA at 4002, 00 at 4003, and FF at 4000.<br>
    To solve these sorts of problems, remember this:  The address used for a group of bytes is the smallest address of the four.  Identify the smallest memory address.  What byte goes that that address if the "big end" (big Endian) or the "little end" (little Endian).  The remaining 3 bytes are filled in sequence.
</details>

## 11.3 -  Portability Problems
When a word is loaded from memory, the electronics puts the bytes into the register in the correct order. Operations (such as addition) inside the processor use the same order. When the register is stored to memory the bytes are written in the same order. As long as the electronics is consistent, either byte order works. Usually you don't need to think about which order is used (and this is really the last time we'll talk about this distinction).

However, when data from one computer is used on another you do need to be concerned. Say that you have a file of integer data that was written by an old mainframe computer. To read it correctly, you need to know (among other things):

* The number of bits used to represent each integer.
* The representational scheme used to represent integers (two's complement or other).
* Which byte ordering (little or big endian) was used.

## 11.4 - Variables in Assembly Programming
Now, let's look at how to add variables to our assembly programs.  Remember that variables are just symbolic names which refer to a memory location where some data is stored.  

Look at the following program skeleton:
```
// Using variables in ARM

.global main

/*** Global vars and static data ***/
.data
x: .word 0 

/*** Code goes in the text section ***/
.text

main:
    push {lr}
    ...
    pop {lr}
```
Notice that we've added another directive section, `.data`.  This section is used for variables and static data.  In that section, we have the code:
```
x: .word 0
```
This is essentially our variable declaraction and initialization.  We define a label (which is the variable name).  In ARM, labels are the symbolic name, followed by a colon.  So `x:` creates a label named `x` and associates it with some memory.  The next directive, `.word` specifys the quantity of memory the label references.  In this case, `.word` instructs the assembler to reserve four bytes of space for the value of the variable `x`.  The `0` at the tells the assembler what pattern to put into those four bytes of memory.  In this case, we want the binary pattern for the value 0.

So the (roughly) equivalent instruction in C would be:
```
int x = 0;
```

We will seee other types of variable including ASCII strings later.

## 11.5 - Loading Values from Memory
The ARM instruction that loads a word into a register is the `ldr` instruction. The store word instruction is `str`. Each must specify a register and a memory address. For this class, an ARM instruction is 32 bits, and an ARM memory address is 32 bits. How can a load or store instruction specify an address that is the same size as itself?

The accessing of variable values from memory must happen in two steps:
1.  Load the address of the variable (say, `x`)
2.  Load the value at that address into a register.

Let's look at each of these in detail.

### 11.5.1 - Getting a variable's address
In ARM, we can can specify we want the address of a variable by placing a `=` in front of the variable.  For example:
```
ldr r1, =x
```
This instruction loads the *ADDRESS* of x into the register `r1`.  It's important to understand that this instruction *DOES NOT* load x's value into the register.  For that, we need a separate instruction,

### 11.5.2 - Loading the value at an address
We now have an address in a register.  We need to instruct the chip to load the 32-bit binary pattern found at that address into a register.  We can do that with the **register direct** addressing mode.
```
ldr r2, [r1]
```
In this case, the brackets around the register, `[r1]` tell the chip to treat what is currently in `r1` as an address, access that memory address, and place the 32-bit pattern found there into the destination register, `r2` in our example.

## 11.6 Storing values to memory
Likewise storing a variable's value to memory must happen in two steps:
1. Load the address of the variable 
2. Store a value located in a register to that address in memory

The first step is the same as that found in section 11.5.1.  However, step 2 requires us to use the `str` instruction:
```
str r0, [r1]
```
This instruction stores the binary pattern currently in `r0` to the memory location whose address is stored in `r1`.  Again, the brackets indicate register direct addressing mode.

## 11.7 - A Complete Example
Here's a complete example using the concept of loading a variable's value from memory, modifying the value, and then updating the variable with the new value.

```
.global main

/*** Data section ***/
.data

x: .word 3

/*** Code section ***/
.text

main:
    push {ip, lr}

    // r0 <- x
    ldr r0, =x
    ldr r1, [r0]

    // add 5 to x's value
    add r2, r1, #5

    //update x's value in memory
    str r2, [r0]

    // Return
    pop {ip, pc}
```

This program is (roughly) the equivalent of this C program:
```
int main() {
  int x = 3;
  x = x + 5;
}
```

A few things to note about this program:

* If we update a variable (ie, assign a new value to the variable), we must store the value back to memory. 
* Since ARM is a load-store architecture, we cannot use register indirect addressing mode as an operand to instructions such as `mov` or `add`.
* In the above example, we load x's address once and store it into `r0`.  As long as we are careful not to modify or overwrite `r0`, we can reuse x's address multiple times, for both `ldr` and `str` instructions.



