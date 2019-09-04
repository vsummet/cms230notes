# Pointers and Arrays

Now that we've seen pointers, let's explore a powerful aspect of pointers.  But first a quick review about how arrays are stored in memory.  Recall that array elements are stored *consecutively* in memory.  In other words, if we have a 5 element integer array, `array[0]` will be "next to" `array[1]` which will be next to `[array[2]` and so on.  Conceptually, the array would look like this in memory if the starting address was 2000 and each integer was 4 bytes (32 bits) long:

```
      |   ...    |
      ------------
2000  | array[0] |
      ------------
2004  | array[1] |
      ------------
2008  | array[2] |
      ------------
2012  | array[3] |
      ------------
2016  | array[4] |
      ------------
      |   ...    |

```
Notice that the addresses of each array element are also consecutive.  Therefore, if we know the starting address of the array and the index of the element we're trying to locate, we can do a bit of math to determine the address of that specific element: 
```
address of array[x] = starting address of array + (x * sizeof(int)) 
```
This makes arrays *incredibly* fast and thus very useful for problems when you need fast computation.

Also, recall that pointers are just addresses.

## Fearful Symmetry

There exists an interesting symmetry between pointers and arrays.

Consider a basic array declaration.

```
int a[5] = {0, 1, 2, 3, 4};
```

Creating this array allocates space in memory for 5 `int` values and binds the name `a` to the memory location where the array begins.

```
   ----------------
a: |      0       |
   ----------------
   |      1       |
   ----------------
   |      2       |
   ----------------
   |      3       |
   ----------------
   |      4       |
   ----------------

Each element represents a single int (4 bytes).
```

Here is the basic symmetry: **the name of an array functions as a pointer to the array's first element**. Therefore, it's possible to access elements of an array using either the traditional `[ ]` notation, or with the `*` dereferencing operator.

```
*a is equivalent to a[0]
*(a + 1) is equivalent to a[1]
*(a + 2) is equivalent to a[2]

etc.
```

Notice the use of parentheses. `*(a + 1)` is not the same as `*a + 1`!

This "+ 1" relationship holds regardless of the type of the array.

```
double dArray[3] = {1.11, 2.22, 3.33};
printf("%f\n", *dArray);  // prints 1.11
printf("%f\n", *(dArray + 1));  // prints 2.22
```

Performing calculations that change the value of a pointer is called **pointer arithmetic**. The fundamental rule of pointer arithmetic is that `a + i` always points to the `i`th element beyond the beginning of array `a`, regardless of its type.

## Pointers to Arrays 

Because the name of an array functions like a pointer, a pointer can be assigned to an array.

```
int *p = a; // Make p point to the beginning of a
```

Notice that the assignment uses `a` and not `&a`: `a` is already functioning like a pointer to a memory location, so it isn't necessary to get its address.

Once an assignment has been made, elements of the array can be accessed using the pointer.

```
printf("*p = %d\n", *p);  // prints 0
printf("p[0] = %d\n", p[0]);  // pointers can use [ ] notation also
    
*p = 100;  // Equivalent to a[0] = 100
printf("Changed first value = %d\n", a[0]);  // prints 100
```

Notice, in the example above, that both `*` and square bracket notation can be used to access elements of an array. The two are equivalent: square bracket expressions are actually converted to pointer expressions by the compiler.

```
a[i] is equivalent to *(a + i)
```

## The Major Difference

There is one key difference between pointers and arrays.

A array's name is **bound** to the location in memory where its data begins, and cannot be changed. Therefore, it isn't possible to make an assignment that would make an array's name refer to a different memory location.

A pointer is simply a variable, however, so it can be reassigned freely.

```
int a[3] {1, 2, 3};
int b[3] = {4, 5, 6};

int *p = a;
p = b;  // No problem

a = b;  // Can't assign to an array! Compiler SMASH!
```
