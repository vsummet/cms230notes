# Data Structures in C - `struct`s

## A Review
In Java, you've worked extensively with objects.  In fact, everything in Java is an object.  You can't get away from them!  As a reminder, objects are containers which group data and behaviors into a single entity.  The data takes the form of variables while the behaviors take the form of methods.  Because the central concept of computation in Java is an object, we say that Java is an *object oriented programming* (OOP) language.

## Moving on
In contrast, C is a *procedural programming* language.  It is built around functions (or procedures).  The structure of a C program derives from a series of function calls.  It turns out, C has a mechanism for grouping **data** together into a single unit for easy reference.  But this grouping cannot contain methods, making it fundamentally different from the concept of objects in an OOP language such as Java or C++ (C's predesessor).  In C, this grouping is called a `struct` (short for structure).  Let's write a `struct` to mimic a book which contains a title, author, and a number of pages:

```
struct book_t {
   char  title[50];
   char  author[50];
   int   pages;
} book;
```

## Details
Let's dive in an look at the pieces of the `struct`.  First we see the line:
```
struct book_t {
```
This defines the template for a `struct` and gives it a unique name.  Just like in Java classes, we use `{ ... }` to indicate where the data to be contained in the struct starts and stops.

The next 3 lines specify what type of data each `struct` will contain (eg what defines a book):
```
   char  title[50];
   char  author[50];
   int   pages;
```
In this case, we see that we've defined an array of 50 characters (a string) to hold the title, another array of 50 characters to hold the author, and an integer to represent the number of pages in the book. 
