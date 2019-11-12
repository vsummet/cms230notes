# Chapter 12 - File I/O

## 12.1 - File Pointers and Opening a File
In C, files are opened as pointers.  The relevant function is:

```
  FILE *fopen(const char *filename, const char *mode);
```
 
This function is included when you include `<stdio.h>` as you do in most programs.
 
The first argument is the path to the file we wish to open. The second argument, `mode`, allows us to open a file for reading, writing, or both.  In general, open a file for reading only unless you really need to write to it.  You should not read from and write to a file at the same time as this can cause problems unless you do it carefully.  The following snippet of code opens a file named `data.txt` in the current directory for reading only.
 
```
 FILE *fp = fopen("data.txt", "r");
```
 
This function returns a pointer if the file opens successfully and `NULL` if it does not.  You usually want to use this return value to check the opening of the file and send up a distress call if it did not open correctly.
 
```
FILE *fp = fopen("file which doesn't exist", "r");
if (fp == NULL) {
 //stop program before it really starts
}
```
Once the file is open, we can read data from it. 
  
## 12.2 - Reading From an Open File
Once we have opened a file and have a file pointer to it, we can use some variants of our old friends `scanf` and `fgets` to read from it.
 
The function `fscanf` allows us to read a single piece of data, up to a whitespace character, from a file.  The function's header is:
```
  int fscanf(FILE *stream, const char *format, variable);
```
We pass our (already opened) file pointer as the first argument.  Then we pass the format specifier of the data we want to read and the variable we wish to store it in.  Thus, ```fscanf(fp, "%d", &x)``` reads an integer from the file referenced by `fp` and stores it to the integer variable `x`.
 
This function returns the number of bytes successfully read from the file.  If the function returns 0, you have a problem (assuming you intended to read some amount of data).
 
If we want to read past a whitespace character, we can use the function `fgets`.  We've already seen this function:
 
```
  char *fgets(char *s, int n, FILE *stream);
```
This function operates just as we've seen before, reading `n` characters from a line or until it encounters a newline character: `\n`.  The only difference is that we now pass our file pointer as the last argument rather than using the `stdin` stream.
 
 
## 12.3 - Writing to an Open File
There are a variety of functions we can use to write to a file.  One of the most useful is `fprintf`.  
 
```
int fprintf(FILE *stream, const char *format, ...);
```
This function allows us to write a formatted string to a file; we simply pass our file pointer as the 1st argument, then a formatted string (including the usual format specifiers), followed by the values.  The code
 
```
 fprintf(fp, "%d\n", x);
```
would print a line containing x's value to the file referenced by `fp`.

## 12.4 `EOF` and Closing a File
 
At the end of the file is a special delimiter known as the **end-of-file** character, commonly written as `EOF`.  We can use this in our code to read until the end of the file

```
int data;
while(fscanf(fp, "%d", &data) != EOF) {
 //process integer data
}
```

This loop structure allows us to do two things at once:
1. read a piece of integer data from the file.  If this fails because we are at the end of the file, `fscanf` returns the special `EOF` indicator.
2. end the loop if we were at the end of of the file and there is no more data to be read

After you have finished reading from a file, you should close it before your program exits.  The function you should use is:
 
```
 int fclose(FILE *stream);
```
 
 We simply pass our open file pointer to the function.  This ensures that all data is written to the file before our program exits which is always a good thing to do.
 
## 12.5 - Putting It All Together
The following program opens a file of integers, reads from it, adds 10 to each number and prints the numbers to a new file.
 
```
int main(void) {
 //open files
 FILE *read_file = fopen("data.txt", "r");
 FILE *out_file = fopen("output.txt, "w");
 
 //check file opening
 if(read_file == NULL || out_file == NULL) {
   printf("Error opening file.\n");
   return 1;
 }
 
 int data = 0;
 
 //read a number and check to make sure we haven't reached the end of the file, all in one loop
 while(fscanf(read_file, "%d", &data) != EOF) {
   data = data + 10;
   fprintf(out_file, "%d\n", data);
 }
 
 //cleanup and close files
 fclose(read_file);
 fclose(out_file);
 
 return 0;
} 
```
