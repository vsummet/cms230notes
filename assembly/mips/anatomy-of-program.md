# Chapter X - Anatomy of a Basic Assembly Program

While assembly programs and high level programs are equivalent (that is, you can program anything in assembly that you would in a HLL), they are quite different in syntax and structure.  It pays to look at the differences with a very short, simple program before launching into more details.

Chapter topics:
* Assembly language directives
* Symbolic addresses
* Run time

## X.1  A basic program and explanation
Here's a basic program to compute 2+3

```
## Program to add two plus three 
        .text
        .globl  main

main:
        ori     $8,$0,0x2       # put two's comp. two into register 8
        ori     $9,$0,0x3       # put two's comp. three into register 9
        addu    $10,$8,$9       # add register 8 and 9, put result in 10

## End of file
```
The first line of the program is a comment. It is ignored by the assembler and results in no machine instructions.

`.text` is a **directive**. A directive is a statement that tells the assembler something about what the programmer wants, but does not itself result in any machine instructions. This directive tells the assembler that the following lines are ".text" -- source code for the program.

`.globl main` is another directive. It says that the identifier `main` will be used outside of this source file (that is, used "globally") as the label of a particular location in main memory.

Blank lines are ignored. 

The line `main:` defines a **symbolic address** (sometimes called a **statement label**). A symbolic address is a symbol (an identifier) that is the source code name for a location in memory. In this program, main stands for the address of the first machine instruction (which turns out to be 0x00400000). Using a symbolic address is much easier than using a numerical address. With a symbolic address, the programmer refers to memory locations by name and lets the assembler figure out the numerical address.  The symbol `main` is global. This means that several source files can use the symbol `main` to refer to the same location in storage. (However, we won't make use this feature. All our programs will be contained in a single source file.)

## X.2  Loading Register Eight
All software consists of interconnected modules. A connection is made when one module refers to an address in another.

The next line: `ori $8,$0,0x2` translates into a 32-bit machine instruction. The machine instruction, upon execution, puts a 32-bit two's complement positive two into register eight (details later).

The instruction after that, `ori $9,$0,0x3`,  translates into a machine instruction that (upon execution) puts a three into register nine. The final instruction translates into a machine instruction that (upon execution) adds register eight to register nine and puts the 32-bit result into register ten.

## X.3 Run Time

It is awkward to keep saying, "The instruction, after it is assembled and loaded into main memory, upon execution does ...."

Instead one says, "At run time the instruction does ..."

For example, "At run time, the instruction `ori $8,$0,0x2` loads register eight with a two.

Even sloppier is, "the instruction `ori $8,$0,0x2` loads register eight with a two."

It is vital that you understand that this phrase is a short way of saying the longer phrase. In a computer it is the bit patterns of machine instructions that cause things to happen, and things happen only at run time.

Sometimes one talks about assembly time, the phase where the assembler is creating bit patterns out of the source file.



