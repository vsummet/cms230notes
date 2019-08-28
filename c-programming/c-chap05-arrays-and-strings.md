# Arrays and Strings in C

Arrays in C act to store related data under a single variable name with an index, also known as a ''subscript''.  As in Java, arrays must contain the same type of data.  That is, you can have an array of It is easiest to think of an array as simply a list or ordered grouping for variables of the same type.  As such, arrays often help a programmer organize collections of data efficiently and intuitively.

Later we will consider the fundamental concept in C: "pointers."  Pointers extend the nature of the array (array can be termed as a constant pointer). For now, we will consider just their declaration and their use.

## Arrays

C arrays are declared in the following form:

```
type name[number of elements];
```

For example, if we want an array of six integers, we write:
```
int numbers[6];
```

For a six character array called `letters`,

```
char letters[6];
```

and so on.

You can also initialize as you declare. Just put the initial elements in curly brackets separated by commas as the initial value:

```
type name[number of elements]={comma-separated values};
```

For example, if we want to initialize an array of six integers with initial values 0, 0, 1, 0, 0, 0:
```
int point[6]={0,0,1,0,0,0};
```

Though when the array is initialized the compiler is smart enough to figure out the dimensions, and will automatically size the array to hold the initial data:
```
int point[]={0,0,1,0,0,0};
```
This is very useful because the size of the array can be controlled by simply adding or removing values from the initialized list  without adjusting the dimension of the array.

If the dimension is specified, but not all elements in the array are initialized, the remaining elements will contain a value of 0. This is useful, especially when we have very large arrays.  This example sets the first value of the array to 245, and the rest to 0:

```
int numbers[2000]={245};
```

### Indexing into an array
Indexing into an array and manipulating individual values in an array is the same as you learned in Java.  However, if you need a review, here you go.

If we want to access a variable stored in an array, for example with the above declaration, the following code will store a 1 in the variable `x`

```
int x;
x = point[2];
```

Arrays in C are indexed starting at 0, as opposed to starting at 1.  The first element of the array above is `point[0]`.  The index to the last value in the array is the array size minus one.

### Bounds Checking - YOUR responsibilty now!
In the example above the subscripts run from 0 through 5. **C does not guarantee bounds checking on array accesses**. Let me repeat that for the back of the room: **C DOES NOT CHECK THE ARRAY BOUNDS**.  This is one of the most important things you can remember about defensive programming in C.  The compiler may not complain about the following (though some compilers on some platforms add this functionality as much as possible):

```
char y;
int z = 9;
char point[6] = { 1, 2, 3, 4, 5, 6 };

//examples of accessing outside the array. A compile error is not always raised
y = point[15];
y = point[-4];
y = point[z];
```

### Using `sizeof` for Bounds Checking
During program execution, an out of bounds array access does not always cause a run time error. Your program may happily continue after retrieving a value from point[-1], whatever that value may be. To alleviate indexing problems, the `sizeof()` function is commonly used when coding loops that process arrays.

```
int i;
int array[]= { 3, 6, 9, 12, 15 };
 
for (i = 0; i < (sizeof(array)/sizeof(int)); i++) {
  //do something with array[i]
}
```

`sizeof` returns the number of bytes allocated.  So if we determine the size of a single element of the array using `sizeof(int)` and the total size of the array using `sizeof(array)`, we can determine the number of elements in the array.  Essentially, we code our own bounds checking.  Abstracting this code into a function allows for easy reuse too.

Notice in the above example, the size of the array was not explicitly specified. The compiler knows to size it at five elements because of the five values in the initializer list.  Adding an additional value to the list will cause it to be sized to six, and because of the `sizeof` function call `for` loop, the code automatically adjusts to this change.  Good programming practice is to declare a variable `size, and store the number of elements in the array in it.

```
...
size = sizeof(array)/sizeof(int);
for (i = 0; i < size; i++) {
...
```


### Multi-dimensional Arrays
C also supports multi-dimensional arrays (or, rather, arrays of arrays). The simplest type is a two dimensional array. This creates a rectangular array - each row has the same number of columns. To get a `char` array with 3 rows and 5 columns, we write:
 
```
char two_d[3][5];
```

To access/modify a value in this array we need two subscripts:

```
char ch;
ch = two_d[2][4];
```

or

```
two_d[0][0] = 'x';
```

Similarly, a multi-dimensional array can be initialized like this:
```
int two_d[2][3] = {{ 5, 2, 1 },
                   { 6, 7, 8 }};
```

The number of columns must be explicitly stated; however, the compiler will find the appropriate amount of rows based on the initializer list.


## Strings

C has no string handling facilities built in; consequently, strings are defined as a **null-terminated character array**.

The following declarations are equivalent.

```
char tokyo[] = "Tokyo";
char kyoto[] = {'K', 'y', 'o', 't', 'o', '\0'};
```

The `'\0'` character is a typical representation for the null byte `0x00`. The null byte marks the end of the string. Since C does not keep track of the bounds of the array, it cannot know how many characters make up the string.  Java stores String as an object and keeps track of an array of characters AND the number of characters in that array.  Instead, C takes a different tack.  If requested, C will cheerfully process characters until it encounters the null character, `\0`.

The system automatically appends a terminating `\0` to strings declared with quotes.

Notice, also, that the size of the array doesn't have to be declared if the compiler can infer it from the initial assignment.

Individual letters of the string can be accessed like any other array element.  This is a difference from Java which does not support array indexing and instead requires the use of the `charAt(index)` method.

```
tokyo[0] is 'T'
```


Strings do not always have to be linked to an explicit variable.  As you have seen already, a string of characters can be created directly with no associated variable (as with the `printf` functions.)  


There is a useful library of string handling routines which you can use by including another header file.

```
#include <string.h>  //new header file
```

This standard string library will allow various tasks to be performed on strings, and will discussed later, once we cover pointers.
