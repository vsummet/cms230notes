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
format2: .asciz "%d^%d = %d\n"

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

## Exercise 2: Power
Modify your multiplication program by adding a `power` function. The function should take two arguments, `p` in `r0` and `q` in `r1`, and return `p` raised to the power `q` in `r0`. Use a loop that calls `multiply` to calculate the answer.  Change main so uses the `format2` string and prints out the result of the `power` function.

For this problem, you will need to be careful with register management.  You can use the `push` and `pop` instructions to push temporary values onto the stack before the function call and `pop` to restore them after the call.

For example, let's say you're calculating a value in `r1`, but you need to call a function and use `r1` for to pass an argument to that function.  What to do?  Well, let's push the value of `r1` onto the stack, setup `r1` with the new value needed for the argument value, call the function, then restore the previous value in `r1` after the function returns:

```
push {r1}   //pushes the value in r1 onto the stack
mov r1, #100   //let's say we're passing the value 100 as the 2nd argument to our function

bl function // call our function

pop {r1}  //restore the value from the stack back into r1
```

You can use `push` and `pop` to push/pop multiple register's values on and off the stack.  For example: `push {r1, r5}` will cause both r1's and r5's values to be added to the stack.  

You can also pop the values off the stack and put them into other registers just by changing the registers you specify when using `pop`.  For example:
```
mov r1, #100  //100 in r1
mov r5, #30   //30 in r5
push {r1, r5}  //100 and 30 added to the stack
pop {r2, r6}   // 100 is now in r2 and 30 is now in r6
```

## Submission
Copy/paste your entire program into Mimir.  If you could not get it to work, fill out question 2 and explain how your program does't work or what parts do work (for example, if you got multiplication working put not the power function).
