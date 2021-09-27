# Smart Pointers
- Class type that look and act like a raw pointer but with additional capabilities
- Allows programmer to control the following pointer behaviors:
    - Construction and Destruction: 
    - Copy and assignment    
        - Shallow copy, deep copy, or no copy 
    - Dereferencing
- Primarily used for RAII to make programs using pointers exception safe

## unique_ptr
- Smart pointer that cleans up after itself
- Advantages:
    - Very efficient
    - When it goes out of scope, the destructor frees pointed to object
- Disadvantages:
    - Retains sole ownership of an objct
        - Cannot copy or copy-assign
        - Two instances cannot manage the same object
- Typical uses:
    - Guarantees deletion (helpful for exception safety)
    - Passing ownership of uniquely-owned objects into methods
    - Acquiring ownership of uniquely-owned objects from methods
- Managing ownership:
    - `release()` 
    - `reset()`
    - `swap()`
- Can be used w/ arrays

## shared_ptr
- reference-counting smart pointer
- Track how many objects point to a particular resource
- Deletes the resource when no pointers point to the resource anymore
- assignment and copy construction are how shared_ptrs keep track of the number of references
    - constructing the pointers seperately would result in two different shared_ptrs

``` c++
using std::shared_ptr;
Circle *foo = new Circle();
shared_ptr<Shape> aShape(foo);

shared_ptr<Shape> aNewShape(aShape) // copy constructor creates new smart pointer and increments reference count
aShape = aNewShape; // nothing changes

shared_ptr<Shape> aNewPtr(foo); // creates an entirely new shared_ptr with seperate reference count than the above shared_ptrs
```