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

## Setup
Open Mimir and begin the "Debugging Lab" project.  This should copy the starter code of `gdb_demo.c` into your directory.  Open this file and look at it.  You may see some errors, but don't fix them yet.  Go ahead and compile the file with the `-g` flag:
```
gcc -Wall -Werror -g -o gdb_demo gdb_demo.c
```

## Lab Activities
Since `gdb` is a "supervisor," we have to tell it what executable to supervise:
```
gdb executable_name
```
### Running `gdb`
`gdb` is an *interactive* program which has its own prompt.  You can tell whether `gdb` is currently running by looking for the prompt: `(gdb)`.

Go ahead and run the file you compiled with `gdb`:
```
gdb gdb_demo
```
You should see some output as `gdb` starts up and then you should see the `gdb` prompt:
```
user@mimir: ~ > gdb test_prog
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
Reading symbols from test_prog...done.
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
