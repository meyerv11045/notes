# Strong Exception Safety
- Very large and old software systems with ad hoc resource managment cannot use exceptions.

## noexcept Specfication
- Functions that guarantee they will not throw an exception should specify that like so: `void foo (...) noexcept;`
- Can also be used as an operator that returns true at compile time if a given expression is guaranteed to not throw an exception

## General Principles
- Can design every function to:
    - 1) Complete successfully
    - 2) Fail in a well-defined manner
- Assume every function that can throw an exception will throw one and incorporate it into your code/design
- Never delete a peice of information before the replacement info is ready for use
- Basic Tools:
    - Try-blocks
    - Support from Resource Acquisition Is Initialization (RAII) technique
- Throw and catch exceptions only when absolutely necessary
- When exception is thrown:
    - Leak no resources
    - Don't permit data structures to become corrupted
-  

## Standard Exception Class Heierarchy
```
exception
    logic_error
        domain_error
        length_error
        invalid_argument
        out_of_range
    runtime_error
        range_error
        overflow_error
        underflow_error
```

## Mutex
- **Mu**tual **ex**clusion object
- An object that allows multiple program threads to share the same resource (e.g. file access) but not simultaneously 
- Mutex is locked when being used and unlocked when no longer needed
- `std::lock_guard<std::mutex> mutex(exMutex)` will automatically lock and unlock the mutex when
    - Strong exception safety because mutex will be unlocked if exception is thrown and will not freeze program b/c of never reaching the unlock call
    - Example of using RAII to destroy local variables when they go out of scope

## Exception Safety
Exception safe functions provide one of four guarantees for if an exception is thrown:
1. No Safety- code is in bad place
2. Weak/Basic- everything in function remains in a valid state, but exact state may be unknown
3. Strong- state of program is unchanged
4. Nothrow- function always works and never throws an exception


operating overloading can cause exceptions on user defined types because they are function calls
combining operating overloading with templates makes things very complicated depending on whether the type is a primitive or user defined

## RAII
- Only code guaranteed to be executed after an exception is thrown are the destructors of objects residing on the stack (local variables)
- Vital to writing exception safe C++ code
    - REquired so resources are released before permitting exceptions to propagate
