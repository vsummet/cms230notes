# Using `gdb` to Debug

## Background
There's no way around it: debugging is programming. You will spend more of your time debugging than actually writing code. Even very experienced programmers spend a significant time debugging. Furthermore, even if you write rock solid code, chances are you are going to be using libraries and system calls written by someone else. So you can also end up debugging problems surrounding the interfaces between your code and other code.

You've probably debugged using `print` statements in the past.  You print out the values of variables at different points in the code and try to find where it's going wrong.  This is very useful, but sometimes insufficient, particularly when working with a new language and trying to understand its quirks and foibles.  A debugger allows you to do the same things, but without modifying and re-compiling your code.

### `gdb`
The GNU debugger (`gdb`) is a very popular command-line tool for stepping through and analyzing C code. It can also be used with other languages such as C++ and assembly, but for this lab, we will use `gdb` to debug some user-level C code.  Other IDEs and programming environments will have other debuggers.  But usually, the concepts and ideas remain the same regardless of which debugger you're using.

A debugger is a sort of "supervisor." It has full control of your program: it can pause, resume, run it step-by-step, look at all the variables, change all the variables, etc. Probably the most important thing a debugger can do is pause with something called a **breakpoint**. A breakpoint is a way of telling the debugger, "when my program gets to this line, stop!" Once the program is paused, you can look at everything, see where you are, see what went wrong, and so on.

The debugger also saves the state of your program and can allow you to look at what happened immediately before your program crashed.  Often, student programs crash due to a common exception, the **segmentation fault**.  These almost always occur when you dereference a NULL or bad pointer.

`gdb` is most useful in finding out how a program is executing by watching the program flow and by inspecting the values of variables at run time. Although `gdb` is very sophisticated, you only need to learn a small subset of the commands in order to make it useful. 

### How does `gdb` work?
When we compile an source code to an executable, most of the "squishy human" things like variable names, function names, references to the C source code etc. are thrown away. The CPU doesn't need or care about them, and they would just waste space in the executable file.
But we can tell gcc to include that information with the `-g` flag:
```
gcc -Wall -Werror -g -o executable_name source_code.c
```
Now, when we run our program inside `gdb`, it’ll be much easier to debug as you will be able to map it to the source code you are working with.

### Linked lists
Linked lists are a fundamental data structure and show up on lots of technical interviews.  If you've forgotten the basics of linked lists, I recommend you watch (https://www.youtube.com/watch?v=VOpjAHCee7c)[this video].  It covers the conceptual idea of linked lists as well as an implementation in C.  After about 14:30 he covers implementation in Java, which isn't relevant for us in this course.  The video is fast paced, but make sure you understand the concept of linked list as well as the fact that the last node in the list points to `NULL`.

## Setup
Open Mimir and begin the "Debugging Lab" project.  This should copy the starter code of `gdb_demo.c` into your directory.  Open this file and look at it.  You may see some errors, but don't fix them yet.  Go ahead and compile the file with the `-g` flag but don't use the -Wall -Werror flags!
```
gcc -g -o gdb_demo gdb_demo.c
```
Go ahead and run it and then type in a number.  You should see the output:
```
user@mimir: ~ > ./gdb_demo
Enter a number: 3
Segmentation fault (core dumped)
```
Seg faults are something `gdb` can help us find and diagnose!

## Lab Activities
Since `gdb` is a "supervisor," we have to tell it what executable to supervise:

```
gdb executable_name
```

`gdb` is an *interactive* program which has its own prompt.  You can tell whether `gdb` is currently running by looking for the prompt: `(gdb)`.

### Part 1 - `gdb` with easy code
Go ahead and run your executable file (**not** the source code!) with `gdb`:
```
gdb gdb_demo
```
You should see some output as `gdb` starts up and then you should see the `gdb` prompt:
```
user@mimir: ~ > gdb gdb_demo
GNU gdb (Ubuntu 8.2-0ubuntu1~16.04.1) 8.2
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from gdb_demo...done.
(gdb) 
```
### Issuing Commands to `gdb`
At this point, you have to tell `gdb` what you want it to do.  Here are some of the most common `gdb` commands, the shortcut for running them, and what they do.  You can get help on any command by typing `help command` at the `(gdb)` prompt.

| Command       | Shortcut  | Description |
| ------------- |:---------:| ----------- |
| help          |           | Get help on a command or topic |
| set args      |           | Set command-line arguments |
| run           | r         | Run (or restart) a program |
| quit          | q         | Exit gdb |
| break         | b         | Place a breakpoint at a given location |
| continue      | c         | Continue running the program after hitting a breakpoint |
| backtrace     | bt        | Show the function call stack |
| next          | n         | Go to the next line of source code without entering a function call |
| step          | s         | Go to the next line of source code, possibly entering a new function |
| nexti         | ni        | Go to the next instruction without entering a function call |
| stepi         | si        | Go to the next instruction, possibly entering a new function |
| print         |           | Display the value of an expression written in C notation |
| x             |           | Examine the contents of a memory location (pointer) |
| list          |           | List the source code of the program |
| disassemble   | disas     | List the machine code of the program |

## Finding our Seg Fault
To begin with, we'll simply run our program, so type "run" or "r" at the `(gdb)` prompt.  You'll be prompted to enter a number, just as if you were running the program as you normally do.  Go ahead and type a number.    You should see output like:
```
(gdb) run
Starting program: /home/valerie/gdb_demo 
Enter a number: 3

Program received signal SIGSEGV, Segmentation fault.
0x00007ffff7a6cde5 in _IO_vfscanf_internal (s=<optimized out>, 
    format=<optimized out>, argptr=argptr@entry=0x7fffffffe1f8, 
    errp=errp@entry=0x0) at vfscanf.c:1902
1902    vfscanf.c: No such file or directory.
(gdb) 
```
Notice that we are back at our `gdb` prompt -- marked with `(gdb)` -- and ready to give `gdb` more commands.

`gdb` is telling us where the program crashed, but it is an odd function name: `vfscanf`. We see
the `scanf` part and might assume that it's a problem with our input, but to be sure,
let's find out by asking for a *backtrace* which will print the series of function calls that got us to the place where the program crashed.  Type `backtrace` or `bt` at the `(gdb)` prompt.
```
(gdb) bt
#0  0x00007ffff7a6cde5 in _IO_vfscanf_internal (s=<optimized out>, 
    format=<optimized out>, argptr=argptr@entry=0x7fffffffe1f8, 
    errp=errp@entry=0x0) at vfscanf.c:1902
#1  0x00007ffff7a785df in __isoc99_scanf (format=<optimized out>)
    at isoc99_scanf.c:37
#2  0x0000000000400643 in main () at gdb_demo.c:18
(gdb) 
```
This is the equivalent of a stack dump when we get an exception in Java called the **activation records** on the stack.  `gdb` lists them in backwards order. So we’re in `_IO_vfscanf_internal`, which was
called by `scanf`, which was called by `main`. But we don’t know anything about the internals of `scanf` and friends,
so we can ignore those lines. The important one is:
```
#2  0x0000000000400643 in main () at gdb_demo.c:18
```
This tells us that the code that crashed is on line 18 of the file `gdb_demo.c`.
Let's find out what's at line 18 by
using the list command which also requires the filename and line number.  Type `list gdb_demo.c:18`  (note: don't confuse this with the standard Linux command `ls`).
```
(gdb) list gdb_demo.c:18
13  int main() {
14          int x;
15          char c[30];
16
17          printf("Enter a number: ");
18          scanf("%d",x);
19
20          fun();
21
22          return 0;
(gdb) 
```
Oops, there's no ampersand on the variable `x`. Quit `gdb` by using the `quit` command.
```
(gdb) quit
A debugging session is active.

    Inferior 1 [process 164] will be killed.

Quit anyway? (y or n) y
user@mimir: ~ > 
```
Now add the ampersand so the code on line 18 now reads:
```
scanf("%d", &x);
```
Recompile the program.  Remember to include the `-g` flag, or better yet, use the up arrow. Run it.```
```
user@mimir: ~ > gcc -g -o gdb_demo gdb_demo.c 
user@mimir: ~ > ./gdb_demo
Enter a number: 3
Floating point exception (core dumped)
user@mimir: ~ > 
```
It crashed again!  Let's run it through `gdb` and see what's going on this time.
```
(gdb) run
Starting program: /home/valerie/gdb_demo 
Enter a number: 3

Program received signal SIGFPE, Arithmetic exception.
0x00000000004005ec in fun () at gdb_demo.c:9
9           c = a / b;
(gdb) 
```
This time it even shows us the exact line of our code which did the crashing.  Because we compiled with the `-g` flag, we can inspect the local variables and see what happened using the `print` command:
```
(gdb) print a
$1 = 5
(gdb) print b
$2 = 0
(gdb) print c
$3 = 32767
(gdb) 
```
Oh, I'm dividing by zero. Let’s try stepping through the code line by line to see how that happens.
I know that my function named `fun` is crashing, so what I’ll do is set a **breakpoint** on `fun`.  This will pause the code before it executes the function.
```
(gdb) break fun
Breakpoint 1 at 0x4005da: file gdb_demo.c, line 4.
(gdb) 
```
You can also set breakpoints using the file name and line number if you have multiple files in your program: `break gdb_demo.c:4`.  Breakpoints are one of the most powerful concepts in any debugger.  You can read more about (http://www.unknownroad.com/rtfm/gdbtut/gdbbreak.html)[commands to manipulate breakpoints] (which will come in very handy on future projects.

Now, I can restart the program with `run` (type `y` to confirm you really want to start the program over) and it'll run like last time, but it'll pause when we get into `fun`.
```
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /home/valerie/gdb_demo 
Enter a number: 3

Breakpoint 1, fun () at gdb_demo.c:4
4           int a = 5;
(gdb)
```
Okay: we've paused. It says we're on the `int a = 5;` line. This is the line that is **about to be executed**. Let's
execute that line and go to the next one with the command `next` (or the shortcut `n`).
```
(gdb) next
5           int b = 0;
(gdb) 
```
Well, duh. We set b to 0.

We can allow the program to resume execution with the `continue` command (shortcut `c`).  Continue causes the program to run until it encounters another breakpoint or it ends (crashes).  As we expect, our program ends with a crash:
```
(gdb) continue
Continuing.

Program received signal SIGFPE, Arithmetic exception.
0x00000000004005ec in fun () at gdb_demo.c:9
9           c = a / b;
(gdb) 
```
We now know where to fix our program to avoid the crash.

### Part 2 - `gdb` with pointers
Now we're going to kick it up a notch.  Let's use `gdb` to investigate some pointer problems. Take a look at   `gdb_pointers.c`.  The program makes a short linked list of 5 nodes (with the values 5, 4, 3, 2, and 1) and then prints them out.  

Compile `gdb_pointers.c` (remember to use the debugger flag!) and run it.  Notice that the program has a problem. What's going on?  Let's use `gdb` to investigate.  Start `gdb` with with `gdb_pointers` as the executable.

The code is pretty messy, so let's set a breakpoint just before we try to print out the nodes with the call to `print_list` on line 34.`

```
(gdb) b 34
Breakpoint 1 at 0x40062d: file gdb_pointers.c, line 34.
(gdb) run
Starting program: /home/valerie/gdb_pointers 

Breakpoint 1, main () at gdb_pointers.c:34
34      printlist(n1);

```

Great!  The program has now built the list (such as it is) and paused to await further instructions.  Let's take a look at the first node in the list.

```
(gdb) print n1
$1 = (node *) 0x602010
(gdb) 
```
At first glance, this doesn't appear to be too useful.  However, remember that `n1` is a `node*` -- in other words, it's a pointer.  We can tell it's value is `0x602010`.  In other words, the pointer isn't `NULL`.  This is a good thing because if we try to derefernece a NULL pointer, bad things happen.  But let's get some more information:
```
(gdb) print n1->value
$2 = 1
(gdb) print n1->next
$3 = (struct node_t *) 0x602030
(gdb) 
```
We can use our right arrow notation in `gdb` too!  Cool.  Even better, we can derefernce our pointers and receive information about all the fields in our struct:
```
(gdb) print *n1
$4 = {value = 1, next = 0x602030}
(gdb)
```
Repeat these steps to inspect `n2, n3, n4,` and `n5`
```
(gdb) print *n2
$5 = {value = 0, next = 0x602050}
(gdb) print *n3
$6 = {value = 0, next = 0x3}
(gdb) print *n4
$7 = {value = 4, next = 0x602090}
(gdb) print *n5
$8 = {value = 5, next = 0x0}
(gdb)
```
Take a look at the addresses for the `next` field.  It looks like we've got some problems with `n2` and `n3`.

Add or modify code to fix `n2->value` and `n3->value`.  Take a look at `n3->next`.  Do you see the error?  Modify this code as well.  Recompile and re-run.  Continue until your program prints out:

`1->2->3->4->5->NULL`

## Recap
When we find a program with a bug, we can interactively debug it using a program like `gdb`. We needed to
compile our executable specifically with the `-g` option to get the extra debug information included in the executable. Once we
did that, we could run the program through `gdb`. `gdb` provides a variety of commands to help us determine the
value of variables and the flow of execution. We examined only a few of the essential commands such as `print`,
`break`, `run`, `next`, and `continue`.  We also learned a few tricks for examining structs and pointers.
