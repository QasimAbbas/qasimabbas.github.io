---
layout: post
title: Ultimate Systems Programming Guide
---

# Ultimate Systems Programming Study Guide

## Syntax

### Types

* For primitives there are different types in C with different sizes and uses
* Keep in mind these are all for a 32 bit architecture!!!
  * int
    * Integer 4 bytes long
  * double
    * More precise number with floating point 16 bytes looking
  * float
    * A number with a floating point half the size of a double 8 bytes long
  * char
    * A character that is 1 byte long

```c

```

### Declaration of Variables and Functions
* Primitives are declared normally
* Functions are still created in a similar way

* These are both placed on the Stack

```c

int i = 0;
char c = 'C';

int main(int argc, char * argv[]){
  char *message = Hello;
  printf(%s, message);

  return;
}

```
### Pointers
* Variables who are addresses to other Variables
 * Helps point to the same variable in memory


### Arrays
* There are different ways that Arrays are handled in C
* Arrays can be dereferenced in two different ways
  * [] brackts like a regular array
  *  using a pointer dereference

* If you have an Array:

```c
//Access Element in Double Array
s[0][0]

//Dereference Double Pointer
**s

//Deference Pointer of Element of an Array
*s[0]
```
* All do the same thing

### Addresses
* What is contained in &y?



### Union

* Store Different datatypes in the same location in memory
* Can be defined with different members but only one can be used at a time

```c
union money{
    char *currency;
    int dollars;
    double price;
};
```

* Allocates to the biggest size, in this case

```c
union money qasim;
qasim.money = "my money"    
qasim.dollars = 12
qasim.price = 12.46
```

* The only thing allocated is price
* Keep track of the datatypes!
### Structs
* Struct is a user defined data type to hold a collection of data types.
* When structs are initialized, they are stored contigiously in memory.
* All members of the struct are initialized and allocated the struct is initialized.

```c
struct person{
    int eyes;
    int nose;
    int mouth;
};
```
* Using a struct
```c
struct person qasim;
qasim.eyes = 2;
qasim.nose = 1;
qasim.mouth = 1;
```

### Enumerated Types
* Enumerated types (enum) are quite different from struct and unions. An enumerated type is a data type where every possible value is defined as a symbolic constant. Enumerations do not have members. Structures do not define lists of constants. A structure can contain enumerations, but an enumeration cannot contain structures.

```c
enum bool{
    false,
    true
}
```

*    Using the Enum
```c
    bool yes = true;
    if(yes){
        printf("IT WORKED :)");
    }
```
### Function Pointer
* Instead of referring to data values, a function pointer points to executable code within memory.

```c
int my_function(int a, int b)
{
    return a + b;
}
```
* Function to be pointed to

```c
int my_function(int a, int b)
{
    return a + b;
}
int main()
    {
    int (*intpointer)(int, int) = NULL;
    intpointer = &my_function;
    int ans = (*intpointer)(1, 2);
    printf("MY ANSWEEWEWWEWERRR %d", ans);

    return 0;
}

```

## Memory

### Dynamic Memory Allocation - Malloc
* Allocates requested size of bytes and returns a pointer to the first byte of allocated space
* Dyanmically allocates Memory in the Heap of a size that is allocated at runtime
```c
int *num = (int *)malloc(sizeof(int));
//Allocated a pointer of type int with a size of int
```
* When there is not enough memory, malloc fails and returns a null pointer
### Calloc
* Allocates space for an array of elements, initializes all the bytes to zero

```c
type *name = (type *)calloc([amount], [size]);
int *num = (int *)calloc(4, sizeof(int));
```
* When there is not enough memory, calloc fails and returns a null pointer
### Free
* Deallocates the amount of memory allocated dynamically

```c
int *num = (int *num)malloc(sizeof(int));
free(num);
```

### Realloc
* Change the size of previously allocated space(this will free the pointer that you give it while it reallocates the space--careful when using).
* Used for resizing previously allocated space

```c
int main()
{
   char *str;
   /* Initial memory allocation */
   str = (char *) malloc(15);

   /* Reallocating memory */
   str = (char *) realloc(str, 25);
   free(str);

   return(0);
}
```
* When there is not enough memory, realloc fails and returns a null pointer

### Segmentation Fault
* You should never free a pointer that has been freed
* Because then we’d have a dangling pointer which can result in unpredictable behavior. This can lead a lot of issues for example security issues or can cause your program to crash.

```c
char * name = (name *)malloc(sizeof(char));
free(name);
free(name);
GAHHH I DIED
```

### Memory Layout

| MEMORY LAYOUT |
|:-------------:|
|Kernel|
|Stack|
|Memory Map|
|Heap|
|BSS|
|Data|
|Text|

#### Kernel
* OS and Processes

#### Stack
* local variables, passing arguments

#### Heap
* dymnamically allocated variables

#### BSS
* undeclared global variables and what not

#### Data
* declared and initialized variables

#### Text
* instructions after compilation

#### Memory Alignment
* When variables are allocated they have padding
 Ex: Allocating a struct on 32bit architecture
```c
struct penguin{
    char name;
    int fish;
    float calories;
}
```
Allocated 13 bytes
Has 16 bytes
3 bytes added for padding
Order dependant


### Implicit vs Explicit Lists

#### Implicit List
* Uses lengths to link blocks in memory
* Need to identify whether block is free of allocated
* Uses the length to move to the next free block
* Use size to traverse in memory
* list abstraction

#### Explicit List
* Node to the next free block
* Won't have free bit
* Will have pointer to the next free block
* Will have free blocks for look for sizes wanted

### Algorithms of Malloc
#### Metadata
* Information of the data in a block of memory that is dynamically allocated

#### Fits
*  First Fit
    * First Available block that fits malloc size
*  Best Fit
    * Block that fits best
*  Worst Fit
    * Opposite of Best Fit
*  Next Fit
    * After first space that fits is found, look for next space that fits
    * Saves you from looking at spaces you've already allocated in the beginning, forces you to look at space near the end

## Concurrent Programming
