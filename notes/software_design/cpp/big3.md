# Classes
- Separate the public interface from the specifics of the implementation
- Everything is private by default (public in a struct)
- public interface provides the abstraction
  - Encapsulation separates the implementation details from the public interface 
    - Data Hiding- one of type of encapsulation where we use private data members/functions

## Base Member Initialization List
Every variable will be constructed before getting into the body of the constructor as a result of the compiler. Therefore we want to use the BMI to prevent doubling the work. Initialize all variables in the BMI (lots of things are able to be initialized including arrays). Order of initialization in BMI should be the same as order declared in the header (compiler doesn't care but good for consistency).

Note the upper most base class is always initialized first.

Initialization is the process of turning raw storage into an object.
Assignment is the process of replacing the existing state of a well-defined object with a new state (never performed on raw storage).

## Big 3
1. Destructor
2. Copy Constructor
3. Copy Assignment Operator

When one of the big 3 needs custom behavior, all of them probably will. Best practice to explicitly define the behavior of the big 3 even if it uses default functionality (serves as documentation).

[Resource](https://gcallah.github.io/OOP2/big3.html)

## Destructor
**Purpose:** destroy items that are allocated onto the heap

- Default destructor does not cause memory leaks for primitve data types.
- Default destructor causes memory leaks when using pointers in complex data types because the data at the allocated memory address is not freed up (memory leak)
- Should not be called explicitly
    - Called by compiler when object goes out of scope or when `delete` is called on an object
- Called in reverse order of the constructors for a heierachy of base classes

## Copy Constructor
**Purpose:** Creates a new object instance with same values as existing object

Different from the assignment operator in that it creates a new object instead of just setting existing objects to be equal to another

Copying involves allocating memory for the data members and then initializing the data members to be the same as those of the referenced object.

Called in 3 instances:
1. Traditional use
   ``` c++
      SomeClass a;
      SomeClass b(a);
   ```
2. Assignment operator is not called because `b` hasn't been initialized
   ``` c++
      SomeClass a;
      SomeClass b = a; 
   ```
3. Passing or returning an object by value creates a copy of that object

Default copy constructor does member wise copy which results in a shallow copies when dealing with pointers. Therefore, we define our own copy ctor for most classes we write

**Example Copy Constructor:**
An object of the same type is passed by constant (don't want to change existing object) reference (can't be passed by value since that would require copy constructor).
``` c++
SomeClass(const SomeClass &rhs ) 
{
      // Any pointer manipulation to prevent shallow copies     
}
```

## Copy Assignment Operator
**Purpose:** set an existing object to be the same as another existing object of the same type

Often overloaded to eliminate the problems caused by memberwise assignment when using pointers.

Assignment involves:
1. Check for self assignment (assignining an object to itself)
2. Deleting the original items stored in the object's data members 
3. Allocating memory for new items
4. Copying the other object's data members to the current object 
   - Best practice to use copy constructor to keep code DRY
5. Return the object (allows for chaining assignment operators)

## Specifying Default and Delete Behavior
- Set copy ctor or assignment operatort to equal `delete` in the header to make it clear the user should not use them
    - Will generate a compiler error if used
    - Prevents the compiler from generating default implementations
    - Certain cases (e.g. cout and files) its not acceptable to make copies or assignments
      
```c++
Stack(const Stack &rhs) = delete;
Stack &operator=(const Stack &rhs) = delete;
```
- Set copy ctor or assignment operatort to equal `default` in the header to make it clear the compiler will generate default implementations
    - Serves as good documentation for user of the class
```c++
Stack(const Stack &rhs) = default;
Stack &operator=(const Stack &rhs) = default;
```

## Garbage Collection
- A program's executable includes automatic behavior that at various intervals finds all unreachable allocated memory locations (e.g., by comparing all reachable memory with all previously-allocated memory), and automatically frees such unreachable memory
- Can reduce the impact of memory leaks at the expense of runtime overhead
- Not implemented in standard C++ but is used in higher-level languages like Python and Java
    - All C++ does is call destructor when variables/objects go out of the scope they were initialized in 
        - Therefore, C++ doesn't call the destructor on reference variables passed into functions when that function's scope ends
    - Destructors for primitive data types works fine but destructors for more complex objects must be defined by user
