# Pointers

A pointer is an object that refers (points) to some object or function, which simply means that a pointer is the memory address of some object or function.

<div style="margin: auto; width: fit-content;"><img src="Images/ptr.png" alt="pointer" style="zoom:200%;" /></div>

<div style="font-size:14px; color: grey;">( Addresses here are shown as integers but in actual systems they will be in hexadecimal.) </div>

To create a pointer we prefix the ampersand symbol `&` to a variable or function name.

For example, suppose we have `int a = 10;` then using `&` with the variable `a` will give the address where the value `10` is stored. If we want to print the address using `printf`, we need to put the pointer format specifier `%p`. It prints the memory address in hexadecimal.

```c
#include <stdio.h>
void main() {
  int a = 10;
  printf("%p\n", &a); // prints the address where 10 is stored
}
```

Output

```
0x7ffdb01f5794
```

## Pointer Variables

Variables that store pointers are known as *pointer variables*. Their data type should be same as the object to which they are pointing.

<img src="Images/ptr_variable.png" alt="ptr_variable" style="zoom:200%;" />

Being a variable, a pointer variable also occupies some memory space. Different implementations of the language allocate different sizes to pointer variables, which restricts the number of memory locations that you may use or access. For example, using an 8-bit addressing mechanism will allow us to access 2^8^ (=256) unique memory addresses and a 64-bit addressing mechanism will allow us to access 2^64^ (=18446744073709551616) unique addresses.

The memory size of a pointer is fixed within a computer or language that you are using, irrespective of the pointer's type. Therefore, a pointer of `int` type, a pointer of `float` type or any other pointer type will have the same  

### Declaration

Declaring a pointer variable is same as declaring any other variable, with just the small difference that variable names (declarators) must be prefixed with an asterisk symbol `*`.

Example: `float *p;`

Here we have declared a pointer variable `p` which can store the address of a `float` variable. 

The  type of a pointer variable must correspond with the type of the object it is going to point. For example if we want it to point to a `float` variable, then we have to define the pointer's type as `float` as well.

As another example, lets declare a pointer variable that will store a pointer to an integer object.  We'll call the pointer variable `p` and its type will be `int`. Also, we will initialise it to point to an `int` variable `a` having value `10`.

```c
#include <stdio.h>
void main() {
  int a = 10;
  int *p = &a;
  printf("%p\n", p);
}
```

In the line `int *p = &a;` above, the address of variable `a` is obtained using the `&` operator and then this address is stored in the pointer variable `p`.

- Formally, a pointer variable declaration has one the given forms:

  `specifiers-and-qualifiers` `*declarators-and-initializers` `;`, or

  `specifiers-and-qualifiers` `*` `declarators-and-initializers` `;`, or

  `specifiers-and-qualifiers*` `declarators-and-initializers` `;`

  <div style="font-size:14px; color: grey;">Note the positions of asterisk.</div>

- For multiple declarators: 

  `specifiers-and-qualifiers *declarator1, *declarator2, ...;` `;`

where,

- `specifiers-and-qualifiers` are a list of type specifiers, type qualifiers and storage-class specifiers. They specify the type of object that the pointer is mend to point.
- `declarators-and-initializers` are a comma-separated list of declarators (the variables we are declaring) and each of them must have an asterisk prefix. They may be accompanied by initializers.

### De-referencing

De-referencing helps us to access and modify the values kept at an address pointed to by a pointer. To de-reference a pointer, we use the de-reference operator `*`.

Suppose we have an integer variable `a` with value `10`,

`int a = 10;`

and we have stored the address of `a` in a pointer variable named `p`. 

`int *p = &a;`

Now how do we use the address stored in `p` to access the variable `a`? In other words we want to access the object `a` using its reference.

We do this by prefixing the de-reference operator `*` to the pointer variable `p`. We write `*p` which means the 'object at location `p`', that is `a`. Using `*p` we can do all operations that we could with `a`. 

As an example let's examine the following code. 

```c
#include <stdio.h>
void main() {
  int a = 10;
  int *p = &a;
  
  // access
  printf("%d\n", *p); // -> 10

  // modify
  *p = 20; // changes the value stored in a
  printf("%d\n", a); // -> 20
}
```

Here, we first print the value stored at the address pointed by `p` (which is `a`'s value), and then we change the value stored at that address by assigning `20` to de-referenced `p`. This changes the content of  `a` which we see by printing `a`'s value.

## Operators

We can use the following operators with pointers.

| Operator | Operator name                 | Example | Description                                                  |
| :------- | :---------------------------- | :------ | :----------------------------------------------------------- |
| `*`      | pointer de-reference          | `*a`    | de-reference the pointer **a** to access the object or function it refers to |
| `&`      | address of                    | `&a`    | create a pointer that refers to the object or function **a** |
| `->`     | member access through pointer | `a->b`  | access member **b** of struct or union pointed to by **a**   |

## Null pointers

A pointer referring to nothing is called a null pointer.

Pointer variables of every type have a special value known as null pointer value of that type. A pointer whose value is null does not point to an object or a function, and compares equal to all pointers of the same type whose value is also null.

To initialise a pointer variable to null or to assign the null value to an existing pointer, a null pointer constant (`NULL`, or any other integer constant with the value zero) may be used.

```c
char *ptr = NULL;
```

Null pointers can indicate the absence of an object or can be used to indicate other types of error conditions.

## Array Pointers

In C, there is a strong relationship between pointers and arrays. The name of an array is itself a pointer to its first (0th) element, so we can access, modify and traverse an array using pointer arithmetic. Basically, any operation that can be achieved by array sub-scripting can also be done with pointers. The pointer operation will in general be faster.

### Access and Modification

Pointers can be used to access and modify array members. For example, lets take the array `int a[] = {5, 10, 15, 20};`.

To *access* the 3rd array element using the sub-script notation we write `a[2]`. Same can be done using pointers by writing `*(a+2)`, which is a way of saying — de-reference the address that is 2 address units ahead of the base address `a`. 

The table below shows side by side comparison of accessing elements by subscripts and pointers.

| subscript notation |  pointer notation  | Value |
| :----------------: | :----------------: | :---: |
|       `a[0]`       | `*a` or `*(a + 0)` |   5   |
|       `a[1]`       |     `*(a + 1)`     |  10   |
|       `a[2]`       |     `*(a + 2)`     |  15   |
|       `a[3]`       |     `*(a + 3)`     |  20   |

Using the same access notation we can also *modify* the array values. For example, `*(a + 1) = 100` will be equivalent to `a[1] = 100`. After this operation `a` becomes `{5, 100, 15, 20}`.

### Traversal

If `p` is a pointer to some element of an array, then `p++` increments `p` to point to the next element, and `p += i` increments it to point `i` elements beyond where it currently does. We illustrate this in the following code.

```c
#include <stdio.h>
void main() 
{
  int a[] = {5, 10, 15, 20};
  
  // a pointer to the first element
  int *p = &a[0];

  p++; // increment
  printf("%d\n", *p); // -> 10

  p += 2; // hop
  printf("%d\n", *p); // -> 20
}
```

## Passing Array to Function

There are two ways of passing an array to a function.

- passing the array name
- passing a pointer to the array

## Pointers to String

In C, we cannot store strings in variables, but we can store a reference to the string in a pointer variable.

When we write something like this,

`char *s = "That's what she said!"`

we assign to variable `s` a pointer (reference) to the first element of the string `"That's what she said!"`.

Something similar happens implicitly in a function call with string arguments. Like in this function call,

`printf("Hello world\n");`

a pointer to the beginning of the character array is passed to `printf`.

However, there is a slight difference between a string literal reference and a character array declaration. Consider these two definitions:

```c
// a_msg is a character array
int a_msg[] = "That's what she said.";
```



```c
// P_msg is a string literal reference
int *p_msg = "That's what she said.";
```

`a_msg` is an array just big enough to hold the sequence of characters and `'\0'` that initialises it. Individual characters within the array may be changed and `a_msg` will always refer to the same storage.

```c
int a_msg[] = "That's what she said.";
a_msg[5] = 'z'; // -> "That'z what she said."
```

On the other hand, `p_msg` is a pointer, initialised to point to a string literal; the pointer may subsequently be modified to point elsewhere, but **the result is undefined if you try to modify the string constant using the pointer**.

```c
int *p_msg = "That's what she said.";
p_msg[5] = 'z'; // error: seg fault
```

## Structure Pointers

A structure pointer is a pointer pointing to a structure, meaning that it is the address of the beginning of a structure. We can obtain it using the 'address of' `&` operator on a structure variable and store it in a pointer variable of the same structure type.

```c
struct Thing {
    int member1, member2;
};

struct Thing t = { 10, 20 };
struct Thing *p = &t; // p refers to t
```

Note: A pointer to a struct can be cast to a pointer to its first member. Likewise, a pointer to the first member of a struct can be cast to a pointer to the enclosing struct. 

## Pointers within Structure

to-do






# Array

Array is a type consisting of a contiguously allocated nonempty sequence of objects with a particular element type. The number of those objects (the array size) never changes during the array lifetime.

OR,

Array is an indexed sequence of fixed number of contiguously allocated nonempty homogeneous objects under one name.

## Declaration

Before using an array, we need to declare it. In a declaration, we state the array's name, size and type.

Syntax

`type-specifier array-name[expression];`

where, `type-specifier` designates the element type (which must be a complete object type) and `expression` designates the number of elements in the array.

Examples

```c
float a[5]; // declares a float array of 5 floats
int *p[10] // declares an array of 10 pointers to ints
long int b[10]; // declares an array of 10 long ints
char s1[4]; // declares a character array of length 4

struct Student {
    char name[25];
    unsigned int rollNo;
};

struct Student students[10]; //  declares an aray of 10 Student
```

We can declare 3 different types of arrays: 

- Constant size arrays
- Variable length arrays
- Unknown size arrays

Let's see how each one is declared.

### Array of Constant Size

If expression in an array declarator is an integer constant expression with a value greater than zero and the element type is a type with a known constant size, then the declarator declares an array of constant known size.

```c
// integer constants are constant expressions
int n[10];

// enum constants are constant expressions
enum { MAX_SZ=100 };
int n[MAX_SZ];

// sizeof is a constant expression
char o[sizeof(double)];
```

### Variable Length Array (VLA)

If expression is not an integer constant expression, the declarator is for an array of variable size.

Each time the flow of control passes over the declaration, expression is evaluated and it must always evaluate to a value greater than zero), and the array is allocated. Correspondingly, lifetime of a VLA ends when the declaration goes out of scope. 

The size of each VLA instance does not change during its lifetime, but on another pass over the same code, it may be allocated with a different size.

```c
#include <stdio.h>
int main(void)
{
  int n = 1;
  do {
    int a[n]; // re-allocated 10 times, each with a different size
    printf("The array has %zu elements\n", sizeof a / sizeof *a);
  } // leaving the scope of a VLA ends its lifetime
  while (n++ < 10);
}
```

Output

```
The array has 1 elements
The array has 2 elements
The array has 3 elements
The array has 4 elements
The array has 5 elements
The array has 6 elements
The array has 7 elements
The array has 8 elements
The array has 9 elements
The array has 10 elements
```

### Array of Unknown Size

If expression in an array declarator is omitted, it declares an array of unknown size. 

```c
int x[]; // the type of x is "array of unknown bound of int"
int a[] = {1,2,3}; // the type of a is "array of 3 int"
```

The `sizeof` operator will throw an error for array`x[]`, but it will work fine with `a[]`. 

## Initialisation

Initialisation means declaring a variable and assigning value(s) to it at the same time.

We initialise arrays using brace enclosed lists `{...}`.

```c
int x[] = {1,2,3}; // x has type int[3] and holds 1,2,3
int y[5] = {1,2,3}; // y has type int[5] and holds 1,2,3,0,0
int z[3] = {0}; // z has type int[3] and holds all zeroes
```

When an array is initialised with a brace-enclosed list of initializers, the first initializer in the list initialises the array element at index zero, and each subsequent initializer initialises the array element at index one greater than the one initialised by the previous initializer.

It's an error to provide more initializers than elements when initialising an array of known size (except when initialising character arrays from string literals).

```c
int n[3] = {10, 20, 30, 40}; // error: number of characters > array size
```

## Access

* Arrays support indexed access. Elements are accessed using array name with subscripts (or indices) in square brackets `[]`. 

  Syntax: `arrayName[subscript/index]` 

  E.g. `arr[5]`

* The subscript must be an integral value or an expression that evaluates to an integral value.

* We can access any element of an array by varying the value of the subscript into the array. (To access all the elements, we may use a loop.)

* Accessing an array element is a **constant time**`O(1)` operation.

* Indexed access can be used for both peek and modify operations.

## One Dimensional Array

A one-dimensional array (or single dimension array) is a linear array, which means that its elements exist one after another in memory. Accessing its elements involves a single subscript.

![array](3 Arrays.assets/array.jpg)

As an example consider the declaration 

`int arr[10];` 

which declares a one-dimensional array named `arr` of ten integers. 

Here, the array can store ten elements of type `int` . This array has indices starting from zero through nine. For example, the expressions `arr[0]` and `arr[9]` are the first and last elements respectively.

The language specifies that array indices always begin at 0, which is why many programmers will call that element "zeroth" rather than "first".

One dimensional arrays are accessed using the same square bracket notation.

```c
int n[5] = {20, 40, 60, 80, 100};

// accessing the element at index 2
printf("%d\n", n[2]); // -> 60

// modifying the element at index 4
n[4] += 50; // {20, 40, 60, 80, 150}
```

Addressing

In a single dimension array, the element with index `i` is located at the address `B + c × i`, where `B` (base) is the address of the first element of the array and `c` (stride) a fixed constant which equals the size of the element type.

## Multi Dimensional Array

A multi-dimensional array is an array of arrays.

### 2-D Array

Each element in a two-dimensional array is an array. We can visualise it as a table or matrix where the two dimensions are rows and columns. 

![2darray](3 Arrays.assets/2darray.gif)

Initialisation

```c
// array of 2 arrays of 3 ints each
int a[2][3] = {{1,2,3},  // can be viewed as a 2x3 matrix
               {4,5,6}}; // with row-major layout
```

Access

An element in a 2-D array is accessed using the same two brackets notation. First `[]` gives access to rows and second `[]` gives access to columns.

```c
// row 0,column 3
printf("%d\n", a[0][2]); // -> 3
    
// row 1, column 1
printf("%d\n", a[1][1]); // -> 5
```

### 3-D Array

In three dimensional arrays each element is an array and each member arrays again has multiple arrays as its members.



![3darray](3 Arrays.assets/3darray-1601272654591.gif)

Initialisation

```c
// 3x3x3 cube
int b[3][3][3] = {
    {
        {1, 2, 3},
     	{4, 5, 6},
     	{7, 8, 9}
    },
    {
        {1, 2, 3},
     	{4, 5, 6},
     	{7, 8, 9}
    },
    {
        {1, 2, 3},
     	{4, 5, 6},
     	{7, 8, 9}
    }
};
```

Access

Use the same three brackets notation to access any element of the cube.

```c
// page 1, row 2, column 0 
printf("%d\n", b[1][2][0]); // -> 7
```

## Size of an Array

We can calculate the size of an array by dividing its total size in bytes with the size of the array's element type. We can use the `sizeof` operator to do so.

`sizeof(arrayName) / sizeof(data-type)` or,

`sizeof(arrayName) / sizeof(first-element)` or,

`sizeof(arrayName) / sizeof(*arrayName)`

```c
int arr[5];
int s1 = sizeof arr / sizeof int;
int s2 = sizeof arr / sizeof arr[0];
int s3 = sizeof arr / sizeof *arr;
```

## Character Array (String)

A *string literal*, written as `"A cat"`, and a character array, written as `{'A', ' ', 'c', 'a', 't'}`, are both null terminated sequences of characters. Internally both are same. They end with the null character `'\0'` so that programs can find the end. Because of null, their length in storage is one more than the number of characters.

They may be of any of the following types: `char`, `signed char`,  or `unsigned char`.

![chararr](3 Arrays.assets/chararr.png)

### Declaration

Declaration is the same as it is for other array types.

```c
char s1[4]; // declares a character array of length 4
```

 ### Initialisation

Character arrays can be initialised in two ways.

- **By using brace enclosed list**

  ```c
  char s[3] = {'c', 'a', 't', '\0'}; // s has type char[4] and holds c,a,t and '\0'
  ```

- **By using a string literal**

  A string literal can also be used for initialising a character array. 

  ```c
  char str[] = "abc"; // str has type char[4] and holds 'a', 'b'. 'c', '\0'
  ```

### Character Array Functions

`string.h` header has many useful functions for manipulating character arrays. It offers convenience functions for usual string operations like finding length, comparing, copying, and concatenating.

The string library is a large one, and basically, it has three types of functions:

- the `str` functions manipulate null-terminated sequences of characters;
- the `strn` functions manipulate sequences of non-null characters.
- the `mem` functions manipulate sequences of arbitrary characters without regard to the null character;

Some commonly used functions are listed here:

- `strcat` - concatenate two strings :heavy_check_mark:
- `strchr` - scans to find a particular character
- `strstr` - scans to find a sub-string
- `strcmp` - compare two strings :heavy_check_mark:
- `strcpy` - copy a string :heavy_check_mark:
- `strlen` - get string length :heavy_check_mark:
- `strncat` - concatenate one string with part of another
- `strncmp` - compare parts of two strings
- `strncpy` - copy part of a string
- `strlwr` - coverts string to lowercase
- `strupr` - coverts string to uppercase
- `strrev` - returns the reversed string

We'll see a little more about the ticked ones.

#### `strcat`

This function appends a copy of the null-terminated byte string pointed to by `src` to the end of the null-terminated byte string pointed to by `dest`. The character `src[0]` replaces the null terminator at the end of `dest`. The resulting byte string is null-terminated.

Prototype 

`char *strcat( char *dest, const char *src );`

Usage Syntax

`strcat(dst, src);`

#### `strlen`

This function returns the length of the given null-terminated byte string, that is, the number of characters in a character array whose first element is pointed to by `str` up to and not including the first null character.

Prototype 

`size_t strlen( const char *str );`

Usage Syntax

`strlen(str);`

where, `str` is  

The behavior is undefined if `str` is not a pointer to a null-terminated byte string.

#### `strcpy`

This function copies the null-terminated byte string pointed to by `src`, including the null terminator, to the character array whose first element is pointed to by `dest`

Prototype

`char *strcpy( char *dest, const char *src );`

Usage Syntax

`strcpy(dst, src);`

#### `strcmp`

This function compares two null-terminated byte strings lexicographically.

Prototype

`int strcmp( const char *lhs, const char *rhs );`

Usage Syntax

`strcmp(lhs, rhs)`

Return Value

- Negative value if `lhs` appears before `rhs` in lexicographical order.
- Zero if `lhs` and `rhs` compare equal.
- Positive value if `lhs` appears after `rhs` in lexicographical order.

## Appendix

### Integer constant expression

An integer constant expression is an expression that consists only of:

- operators other than assignment, increment, decrement, function-call, or comma, except that cast operators can only cast arithmetic types to integer types
- integer constants
- enumeration constants
- character constants
- floating constants, but only if they are immediately used as operands of casts to integer type
- `sizeof` operators whose operands are not VLA

### Designator

A designator causes the following initializer to initialise value of the array element described by the designator. Initialisation then continues forward in order, beginning with the next element after the one described by the designator.

```c
// Here n[3] is initialised with 25, rest with 0. 
int n[5] = { 0, [3] = 25 }; // -> 0 0 0 25 0
```
