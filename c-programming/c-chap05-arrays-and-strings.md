### Arrays and Strings in C

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

## Indexing into an array
Indexing into an array and manipulating individual values in an array is the same as you learned in Java.  However, if you need a review, here you go.

If we want to access a variable stored in an array, for example with the above declaration, the following code will store a 1 in the variable `x`

```
int x;
x = point[2];
```

Arrays in C are indexed starting at 0, as opposed to starting at 1.  The first element of the array above is `point[0]`.  The index to the last value in the array is the array size minus one.

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

During program execution, an out of bounds array access does not always cause a run time error. Your program may happily continue after retrieving a value from point[-1]. To alleviate indexing problems, the sizeof() expression is commonly used when coding loops that process arrays.

Many people use a macro that in turn uses sizeof() to find the number of elements in an array,
a macro variously named
"lengthof()",<ref>
Pádraig Brady.
[http://www.pixelbeat.org/programming/gcc/c_c++_notes.html "C and C++ notes"].
</ref>
"MY_ARRAY_SIZE()" or "NUM_ELEM()",<ref>
[[C Programming/Pointers and arrays]]
</ref>
"SIZEOF_STATIC_ARRAY()",<ref>
[[MINC/Reference/MINC1-volumeio-programmers-reference]]
</ref>
etc.

<source lang="c">
int ix;
short anArray[]= { 3, 6, 9, 12, 15 };
 
for (ix=0; ix< (sizeof(anArray)/sizeof(short)); ++ix) {
  DoSomethingWith("%d", anArray[ix] );
}
</source>

Notice in the above example, the size of the array was not explicitly specified. The compiler knows to size it at 5 because of the five values in the initializer list.  Adding an additional value to the list will cause it to be sized to six, and because of the sizeof expression in the <tt>for</tt> loop, the code automatically adjusts to this change.  Good programming practice is to declare a variable <i>size </i>, and store the number of elements in the array in it.
<p>
size = sizeof(anArray)/sizeof(short)
</p>

C also supports multi dimensional arrays (or, rather, arrays of arrays). The simplest type is a two dimensional array. This creates a rectangular array - each row has the same number of columns. To get a char array with 3 rows and 5 columns we write in C
 char two_d[3][5];

To access/modify a value in this array we need two subscripts:

<source lang="c">
char ch;
ch = two_d[2][4];
</source>

or

<source lang="c">
two_d[0][0] = 'x';
</source>

Similarly, a multi-dimensional array can be initialized like this:
<source lang="c">
int two_d[2][3] = {{ 5, 2, 1 },
                   { 6, 7, 8 }};
</source>

The amount of columns must be explicitly stated; however, the compiler will find the appropriate amount of rows based on the initializer list.

There are also weird notations possible:
<source lang="c">
int a[100];
int i = 0;
if (a[i]==i[a])
{
  printf("Hello world!\n");
}
</source>
----

a[i] and i[a] refer to the same location. (This is explained later in the next Chapter.)

== Strings ==
[[Image:Merkkijono.svg|thumb|300px|String "Merkkijono" stored in memory]]
C has no string handling facilities built in; consequently, strings are defined as arrays of characters. C allows a character array to be represented by a character string rather than a list of characters, with the null terminating character automatically added to the end. For example, to store the string "Merkkijono", we would write

<source lang="c">
char string[11] = "Merkkijono";
</source>

or

<source lang="c">
char string[11] = {'M', 'e', 'r', 'k', 'k', 'i', 'j', 'o', 'n', 'o', '\0'};
</source>

In the first example, the string will have a null character automatically appended to the end by the compiler; by convention, library functions expect strings to be terminated by a null character.  The latter declaration indicates individual elements, and as such the null terminator needs to be added manually. 

Strings do not always have to be linked to an explicit variable.  As you have seen already, a string of characters can be created directly as an unnamed string that is used directly (as with the printf functions.)  

To create an extra long string, you will have to split the string into multiple sections, by closing the first section with a quote, and recommencing the string on the next line (also starting and ending in a quote):
<source lang="c">
char string[58] = "This is a very, very long "
                "string that requires two lines.";
</source>

While strings may also span multiple lines by putting the backslash character at the end of the line, this method is deprecated. 

There is a useful library of string handling routines which you can use by including another header file.

<source lang="c">
#include <string.h>  //new header file
</source>

This standard string library will allow various tasks to be performed on strings, and is discussed in the [[../Strings|Strings]] chapter.

== References ==
{{reflist}}

{{C Programming/Navigation|Simple math|Control}}

[[et:Programmeerimiskeel C/Massiivid]]
[[fr:Programmation C/Tableaux]]
[[it:C/Vettori e puntatori/Vettori]]
[[pl:C/Tablice]]
[[fi:C/Taulukot]]
