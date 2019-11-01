# Loops in Assembly
Having learned how to write if statements in assembly, we now turn to loops.  Fortunately, we don't need to learn any new assembly instructions!  Our branching instructions are sufficient to write loops.

## Review
Recall branching from our previous discussion.  We've learned 7 branching instructions: 1 unconditional branch and 6 conditional branches.  These are displayed in the table below.

| Instruction | Meaning | APSR bits |
|-------------|---------|-----------|
| `b`   | always branch | APSR bits are not relevant |
| `beq` | branch on equal | Z bit is 1 |
| `bne` | branch on not equal | Z bit is 0 |
| `blt` | branch on less than | N bit is not the same as the V bit |
| `bgt` | branch on greather than | Z bit is 0 and N bit is the same as the V bit|
| `ble` | branch on less than or equal to | Z bit is 1 and N bit is not the same as the V bit |
| `bge` | branch on greather than or equal to | N bit is the same as the V bit |

We also discussed a general strategy for translating comparison operators from a high level language into assembly: compare the operands and then branch on the opposite condition.

## Loops
In high level languages, we primarily work with 2 types of loops: `while` loops and `for` loops.  These are equally powerful.  That is, anything we write with a `for` loop, we could write as a `while` loop and vice versa.  In assembly language, we really only work with while loops.  We will first understand while loops in assembly and then `for` loops.

## While Loops
Essentially, `while` loops are just the same comparisons as `if` statements, but with repetition.  Let's consider translating some high level while loop like the following into assembly.  This code multiplies two numbers (`x` and `y`) using repeated addition.
```
int main() {
  int x = 4;
  int y = 6;
  int prod = 0;
  int i = 0; 

  while(i < x) {
    prod = prod + y;
    i++;
  }
  return prod;
}
```

The easiest way to begin this program (after setting up the variables) is to code the while loop in assembly *as an if statement*.  In other words, implement just the following in assembly:
```
if(i < x) {
  prod = prod + y;
  i++;
}
```
We know how to do this!  We have to load lot's of addresses and values from memory, but after that, it's just addition.  In assembly:
```
  //load values for x and y which don't change  
  ldr r3, =x
  ldr r4, [r3]    //value of x in r4
  
  ldr r7, =y
  ldr r8, [r7]    //value of y in r8
  
  //load i for the comparison
  ldr r1, =i
  ldr r2, [r1]    //value of i in r2
  
  //if statement
  cmp r2, r3      //compare i and x's values
  bge done        //if condition is false, don't execute body; branch around following statements
  
  //body of if statement
  ldr r5, =prod
  ldr r6, [r5]    //value of prod in r6

  add r6, r6, r8  //add values of prod and y
  str r6, [r5]    //update prod's value in memory
  add r2, r2, #1  //add 1 to i's value
  str r2, [r1]    //update i's value in memory
  
  //end of if statmeent
done:
  ...
```

To make this into a while loop, we just need to repeat it multiple times.  Instead of just executing the body once, we need to execute it multiple times.  We can add a label and an unconditional branch to take us back to that label:

```
  //load x and y which don't change  
  ldr r3, =x
  ldr r4, [r3]    //value of x in r4
  
  ldr r7, =y
  ldr r8, [r7]    //value of y in r8
  
loopstart:
  //load i for comparison
  ldr r1, =i
  ldr r2, [r1]    //value of i in r2
  
  //if statement
  cmp r2, r3      //compare i and x's values
  bge loopend        //if condition is false, don't execute body; branch around following statements
  
  //body of if statement
  ldr r5, =prod
  ldr r6, [r5]    //value of prod in r6
  ldr r7, =y
  ldr r8, [r7]    //value of y in r8
  add r6, r6, r8  //add values of prod and y
  str r6, [r5]    //update prod's value in memory
  add r2, r2, #1  //add 1 to i's value
  str r2, [r1]    //update i's value in memory
  
  b loopstart
  
  //end of if statmeent
loopend:
  ...
```

Notice the uncondition branch: `b loopstart` at the end of the body.  This will take us back to the beginning, and we'll load the new (updated!) value of `i` and begin the comparison of `x` and `i` all over again.  If the comparison is false, we are done with the loop, and we skip to the end of the loop.

Just as in a high level language, it's a good idea to provide meaningful names to your labels.  `loopstart` is better than `l1` or other confusing names.

## Common Mistakes
When writing loops in assembly, there are two common mistakes:
1. Forgetting the unconditional branch at the end of the loop.  The result of this mistake is that the body of the loop only executes once.
2. Not loading and storing variable values correctly.  In the example above, notice how each iteration of the loop loads the values from memory, and then stores updated values (for `prod` and `i`) at the end of the loop.  On the next iteration of the loop, we have to reload `i` and get the updated value.  You can get into trouble (infinite loops) if you sometimes leave values in registers and sometimes load values from memory.

## For Loops
Once you understand how `while` loops work in assembly, you have also mastered `for` loops!  You just have to rewrite `for` loops as `while` loops and then code them up.

For example, the `for` loop:
```
for(int i = 5, i > 0, i--) {
  stmt;
}
```

can be re-written as a `while` loop:

```
int i = 5;
while(i > 0) {
  stmt;
  i--;
}
```

From there, implementation follows the above examples for `while` loops.
