# Branching and Conditional Branching

The power of computers is their ability to repeat actions and their ability to alter their operation depending on data. Modern programming languages express these abilities using control structures. Repeated action (iteration) is done with a while structure. Alternative control paths (alternation) is done with an if-then-else structure.

The machine instructions of the processor do not have these structures, nor does assembly language. When you program in assembly language you must build these structures out of basic assembly instructions. These basic instructions are the `branch` instruction and the conditional branch instructions.

## How a Branch Works
Most modern computers work on what we refer to as the **Fetch-Decode-Execute** cycle.  These three steps: fetching, decoding, and executing instructions happen over and over again.

When a program is executing, its instructions are located in main memory. The address of an instruction is the address of the first byte of the four-byte instruction.

Each machine cycle executes one machine instruction. At the top of the machine cycle, the PC (program counter) contains the address of an instruction to fetch from memory.  On an ARM chip, the PC is stored in the special purpose register R15.  The instruction is fetched into the processor and is prepared for execution.

!(./images/ch12-machine-cycle.gif)

In the middle of the machine cycle the PC is incremented by four so that it points to the instruction that follows the one just fetched. Then the fetched instruction is executed and the cycle repeats. The machine cycle automatically executes instructions in sequence.

When a `b` (branch) instruction executes (in the last step of the machine cycle), it puts a new address into the PC. Now the fetch at the top of the next machine cycle fetches the instruction at that new address. Instead of executing the instruction that follows the branch instruction in memory, the processor "branches" (or jumps) to an instruction somewhere else in memory.

## Symbolic Addresses
How does the processor know what address to load into the PC when a branch instruction executes?  Remember the concept of **labels* which are just symbolic names for addresses.  For example, we've seen the label `main` in our programs:

```
main: 
  push{ip, lr}
  ...
  pop{ip, pc}
```
`main` is used as just an alias to a specific address in our address space.  So the ARM assembly instruction:
```
b main
```
would cause the address of the first instruction in the function `main` to be loaded into the PC.  On the next machine cycle, the processor would fetch that instruction and the flow of execution would proceed from there.

## Neverending Loops

Consider the following portion of an ARM program:

```
...

.data
x .word 0

.text
...
loopstart:
  ldr r2, =x
  ldr r1, [r2]
  add r0, r1, #1
  str r0, [r2]
  b loopstart
```

In this program, the instruction `b loopstart` causes the flow of instruction to change.  The address of the instruction `ldr r2, =x` is loaded into the PC and begins the execution.  In fact, you're probably thinking that this looks a lot like a loop.  It is!  But it's a *never-ending* loop.  The above assembly program is (roughly) equivalent to the following C program:

```
while(true) {
  x = x + 1;
}
```
We have written an infinite loop!  We load x's value from memory, increment that value by 1, and return it to memory over and over and over and over...

So we see that just a simple branch instruction isn't sufficienbt to allow us to write loops and if-then-else control statements.  To do that, we need **conditional branching** instructions.

## Conditional Branching Instructions
A conditional branch instruction branches to a new address only if a certain condition is true. Usually the condition is about the values in two registers. Here is the  beq  (branch on equal) instruction:
```
beq  u,v,addr   # if register $u == register $v
                #     PC  <— addr (after a delay of one machine cycle.)
                # else
                #     no effect.
```
The bit patterns in two registers are compared. If the bit patterns are the same, the PC is changed to the branch address. There is a branch delay slot that follows this instruction (just as for a jump instruction).



