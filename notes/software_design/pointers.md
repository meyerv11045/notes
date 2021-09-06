# Pointers
- A pointer is a variable that contains a memory address
    - Has a data type that indicates the type of data being stored at the memory address
    - Declared using `*` operator like: `int* a;`
- **Refrence Operator:** `&` obtains a variable's memory address
- **Dereference Operator:** `*` retrieves the data at the memory address a pointer stores
- When declared, pointers hold an unknown address until initialized
- To indicate pointing at nothing, use `nullptr`

## Why use them?
Pointers are all 8-bytes (64-bits on 64-bit machines, 32-bits on 32-bit) so it is much more efficient to use memory addresses of large objects like images or videos than to actually move around the object and make copies of it when doing things like passing them to a function.

## Common Errors

### Syntax
**Using the dereference operator when initializing a pointer**
``` c++
int* a;
int b = 20;
*a = &b;    // error b/c using derefence operator
a = &b      // correct
```
The 3rd line is an error b/c `*a` refers to data being stored at the unknown memory address `a` was initialized to. This will set the data at `a` to the memory address of `b` instead of making `a` point at `b`'s memory address.

Note this will note cause a compiler error, just a tricky to find bug.

However, this is valid and perform the desired functionality because `*` is not being used for dereferencing but rather declaring a pointer:
``` c++
int b = 20;
int *a = &b;
```


**Forgetting the `*` before each pointer when declaring multiple on the same line**

``` c++
int* ptr1, ptr2; // ptr1 will be an int pointer but ptr2 will just be an int
int *ptr1, *ptr2; // makes both of them int pointers
```

Good practice to declare one pointer per line to avoid this.

### Runtime 
**Using a derefence operator `*` when the pointer has not been intialized.** This causes undefined behavior meaning the program could crash if the pointer holds an address the program is not allowed to access.


**Dereferencing a null pointer.** This causes the program to crash.



Memory overflow can be dangerous b/c it results in overwriting data anywhere in memory (can be OS, other programs, etc.)
Aliasing- changing the memory address a pointer points to

## Dereferencing
Derefencing a pointer means accessing the value stored at the memory address the pointer contains
```c++
char* p = "abc" // stores 'a', 'b', 'c' in 3 continuous chunks of memory and p points to the location of a

// Pointer arithmetic can be used to access b and c
assert(*p == 'a');  // The first character at address p will be 'a'
assert(p[1] == 'b'); // p[1] actually dereferences the pointer: p + 1 * (size of p in memory)
assert(*(p + 1) == 'b');  // Another notation for p[1]
```

Change data at the address pointed to by derferencing the pointer:
``` c++
*p = 'z' // now the string of chars is zbc
assert(*p = 'z')
```   

Move pointers through the data:
``` c++
++p;  // Increment p so now it points to 'b'
assert(*p == 'b');
```

## Member Access Operator
``` c++
struct SomeStruct {int a;};

SomeStruct s;
SomeStruct* structPtr = s;
structPtr->a = 1;
// is cleaner than:
(*structPtr).a = 1;
```

## Memory Regions
A program's memory usage includes 3 different regions:
1. **Static Memory**- where global & static local variables are allocated
    - Static variables are allocated once and stay in the same memory location for the duration of the program's execution
2. **Stack**- each function call alloocates a new block of memory called a stack frame to holds its local variables. The stack frames are part of the stack
      - Managed by the run-time system 
3. **Heap**- where the `new` operator allocates memory and the `delete` operator deallocates memory
      - Managed by the programmer (aka the free store)

In classical architectures, the stack and heap grow toward each other to maximize the available space

## Arrays 
- Represented internally as a pointer to the first element
- Accessing elements using indexing is actually just using pointer arithmetic
- A variable declared as an array is the same as a variable declared as a pointer
- When passing an array to a function, only the address of the array is copied into the parameter so any changes to the array in the function will cause a change to the original array b/c its shared

## Strings
- represented internally as a character array ending with the null character `\0`
- since it is a character array, pointer arithmetic and everything can be done on strings



## Resources
- [(Reference) Access Operators](https://en.cppreference.com/w/c/language/operator_member_access)
- [(Slides) Pointers](https://cs.stanford.edu/people/eroberts/courses/cs106b/handouts/21-MemoryAndC++.pdf)
- [(Article) Weird Pointer Expressions](https://www.geeksforgeeks.org/difference-between-p-p-and-p/)