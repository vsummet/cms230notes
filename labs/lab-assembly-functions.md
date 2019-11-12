# Lab - Functions in Assembly Language

## Things to Remember

Functions may take up to four arguments in `r0`-`r3`. The first argument is passed in `r0`, the second in `r1`, and so forth. Additional arguments must be passed on the stack.

The return value is always passed in `r0`.

The **called function** (the *callee*) is allowed to change `r0`-`r3`. If the **caller** wants to preserve values in those registers, it must save them by pushing on the stack before the function call and restore them by popping after the function returns.

If the **callee** wants to modify `r4`-`r12`, it must save their original values and restore them before returning.

This calling convention is particularly important when making calls to `printf` in the middle of a program. Always save `r0`-`r3` before calling `printf` and restore them afterwards, except in the special case where you know you don't need to preserve the values!

## Exercise 1: Multiplication Again

Here's a program that performs multiplication in a loop. The two factors are passed in `r0` and `r1` and the product is returned in `r0`.

Implement the program and add a main function that sets up two arguments, calls `multiply`, and prints the result using `printf` and the `format` string declared in the program.

```
.global main
.extern printf

/*** Data section ***/
.data
format: .asciz "%d x %d = %d\n"

/*** Text section ***/
.text

// multiply(a, b): multiply two values in a loop
//   Inputs: a in r0, b in r1
//   Outputs: product in r0
multiply:
    push {ip, lr}
    
    // mov a and b to r1 and r2
    // Use r0 for the product
    mov r2, r1
    mov r1, r0
    mov r0, #0
  
  while:
    // Test b > 0
    cmp r2, #0

    // Branch on opposite quality
    // if b <= 0, jump around loop body
    ble end

    // Loop body
    add r0, r0, r1  // prod += a
    sub r2, r2, #1  // b--

    b while // unconditional branch back to top

  end:
    // Return -- product is in r0
    pop {ip, pc}
```
