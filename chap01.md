# Chapter 1 - Introduction

Assembly language is used to write programs in terms of the basic operations of a processor. These notes are in the assembly language 
for the ARM processor chip. We will not cover the entirety of the instructions for this chip -- not even close, in fact!  Modern chips are incredibly complex.  However, these notes use actual ARM hardware in the form of a Raspberry Pi.

The **architecture** of a computer is a logical description of its components and its basic operations. In pure assembly 
language one assembly language statement corresponds to one basic operation of the processor. When a programmer writes in 
assembly language the programmer is asking for the basic operations of the processor. The architecture of the processor is 
visible in every statement of the program.

Pure assembly language is rare. Most application programs are written in a **high level language**. Even when assembly language is used 
it usually has been enhanced. Features are added to it to make it more programmer-friendly. This **extended assembly language** 
includes statements that correspond to several basic machine operations. The ARM extended assembly language does this, but the 
processor chip is still visible.

Programs in high level languages such as C or Pascal are (somewhat) independent of the processor they run on. Programs in 
Java are totally independent of the processor. But in assembly language the program is written totally in terms of the 
processor. This chapter starts our tour of assembly language.

Chapter Topics:
* The Basic Computer Cycle
* Machine Instructions
* Machine Language
* Assembly Language
* Language Translation
* Emulation
* Object Modules and Load Modules
* Separate Assembly

## Review Question:
<details>
  <summary>Q: Do all processor chips have the same architecture? </summary>
  A: No. Each family of processor chip (MIPS, PIC, SPARC, Alpha, Motorola, Intel, et al.) has its own architecture
</details>

