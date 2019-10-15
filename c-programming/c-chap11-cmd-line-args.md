# Command Line Arguments

Many programs in the UNIX/Linux world take arguments from the command line. For example, every time we run `gcc` we type something like:

```
gcc -Wall -Werror -o executable_name source_code.c
```

We're supplying a series of arguments to `gcc` which specify the input source file, the output executable, and flags related to warnings and errors.

Up until now, we've used the `int main(void)` declaration for `main` in our C programs.  But `main` can take two optional arguments:

  - `int argc`, which reports the number of arguments typed at the command line
  - `char *argv[]`, which contains the string representation of each argument

```
int main (int argc, char *argv[]) {
    printf("Number of command line arguments = %d\n", argc);
    
    int i;
    for (i = 0; i < argc; i++) {
        printf("argv[%d] = %s\n", i, argv[i]);
    }
    
    return 0;
}
```

Here's an example of running the program:

```
prompt$ ./command_line_input foo bar baz
Number of command line arguments = 4
argv[0] = ./command_line_input
argv[1] = foo
argv[2] = bar
argv[3] = baz
```

It's clear from the output that the name of the program itself counts as the first argument.

Most functions that take command line arguments have the ability to take their input in any order and still make sense of it. A useful function for processing command line arguments in arbitrary order is `getopt`. 

## `getopt` Usage

`getopt` parses the command line arguments supplied to `main` in `argv`.  To use it, you need to include the `<unistd.h>` file.

`getopt` takes 3 arguments: `argc` and `argv` and a third parameter, a string.  This third argument to `getopt` is a string specifying the flags that it should search for in the `argv` list.

For example, the string `"i:o:"` tells `getopt` to search for "-i" and "-o" flags. The `:` after each letter indicates that each flag is followed by a parameter value (for example, the name of an input file might follow the `-i` flag).
    
The flags can occur in any order. When `getopt` finds a flag, it returns the flag letter as a `char` and the second argument, if it exists, in the special variable `optarg`.

This sounds complicated, but let's look at an example which demonstrates the power of command line arguments as well as the ease of parsing them with `getopt`.

```
// Processing input arguments with getopt
// DSM, 2016

#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    char c;

    //loop while getopt is identifying flags and returning them (stored into the variable c)
    while ((c = getopt (argc, argv, "i:o:")) != -1) {
        //do different things for each flag we find
        
        //notice how getopt uses the variable optarg (which is declared in unistd.h)
        switch(c) {
            case 'i':
                printf("i argument = %s\n", optarg);
                break;
                
            case 'o':
                printf("o argument = %s\n", optarg);
                break;
        }
    }
    
    return 0;
}
