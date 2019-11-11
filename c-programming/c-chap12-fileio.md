# Chapter 12 - File I/O

## File Pointers
In C, files are opened as pointers.  The relevant function is:

```
 FILE *fopen(const char *filename, const char *mode);
 ```
 
 This function is included when you include `<stdio.h>` as you do in most programs.
 
 The second argument, `mode`, allows us to open a file for reading, writing, or both.  In general, open a file for reading only unless you really need to write to it.  You should not read from and write to a file at the same time as this can cause problems unless you do it carefully.
 
 This function returns XXX if the file opens successfully and XXX if it does not.  You usually want to use this return value to check the opening of the file and send up a distress call if it did not open correctly.
 
 ```
 XXX example here
 ```
 
 XXX EoF data here
 
 After you have finished reading from a file, you should close it before your program exits.  The function you should use is:
 
 ```
 int fclose(FILE *stream);
 ```
 
 ## Reading from and Writing to an Open File
 Once we have opened a file and have a file pointer to it, we can use some variants of our old friends `scanf` and `fgets` to read from it.
 
 The function `fscanf` allows us to read from a file.  The function's header is:
 ```
  int fscanf(FILE *stream, const char *format, variable);
 ```
 We pass our (already opened) file pointer as the first argument.  Then we pass the format specifier of the data we want to read and the variable we wish to store it in.  Thus, ```fscanf(fp, "%d", &x)``` reads an integer from the file referenced by `fp` and stores it to the integer variable `x`.
 
 This function returns the number of bytes successfully read from the file.  If the function returns 0, you have a problem (assuming you intended to read some amount of data).
 
 
 
 ## Putting It All Together
 The following program opens a file of integers, reads from it, adds 10 to each number and prints the numbers to a new file.
 
 XXX program here
