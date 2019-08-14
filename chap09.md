# Chapter 9 - Introduction to ARM and Assembly

This chapter discusses how to write and run a small assembly program for ARM. 

## Chapter Topics:
* ARM basics
* Writing an assembly source program
* Assembling and loading a program
* Running a program

### Question (Review)
<details>
    <summary>
  What is a register?
    </summary>
A register is a part of the processor that holds a bit pattern. Processors have many registers.
</details>

## 9.1 - Big Picture 
Computers do a pretty small number of things over and over again: 
* move values from memory to CPU and vice versa
* perform arithmetic & logical operations (add, compare, etc)
* read from memory and write to memory

Every CPU implements a "small" set of basic instructions that describe the set of operations it can perform.

These basic instructions are the machine language or **instruction set architecture (ISA)** of the computer.
An ISA describes what the CPU can do and doesn't specify HOW those capabilities are implemented.  Think of ISAs as an API to the hardware.

The advantages of this are:
* hides complexity of HW details
* allows for backwards compatibility of multiple generations of a particular chipset
* allows manufacturers to keep the same ISA interface, but change the internal HW specifics for performance, new technologies, etc.

Recall that programs written in a high-level language are ultimately converted into machine language instructions to execute on the CPU. Different languages do this differently: Java's process is different than C's is different than python's.

Your Raspberry Pi has ARM chip in it.  ARM the dominates mobile & small device market.  Another major player is Intel and their x86 chips/ISA.

Our goals for this chapter:
* understand how programs execute at machine level
* build a mental model of how programs and system interact
* translate high-level statements into assembly

## 9.2 - Specifics

The ARM has 16 32-bit registers.  They are named `r0`, `r1`, and so on up to `r15`

`r0-r12` are general purpose registers.  This means that they are freely available for programmers to use in any manner they want.  The other registers have special purposes and should not be used willy-nilly by programmers. `r13` is the **stack pointer** and stores the address of the top of the stack.  `r14` is the **link register** and is used during subroutine calls.  `r15` is the **program counter (PC)** which stores the address of the next instruction the CPU needs to fetch, decode, and then execute.


ARM is a load-store architecture
	basic idea: load data into registers from memory, do operations on registers, save results back to memory
