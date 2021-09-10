# Exception Handling
- Purpose: permit the program to catch and handle errors rather than let it occur and suffer the consequences
- Used when system can recover from the error causing the exception
- Exception Handler- Recovery procedure

``` c++
try {
    throw std::overflow_error("overflow error in push")
}
catch (std::overflow_error &excep) {
    std::cout << excep.what() << std::endl;
}
catch (...) {
    std::cout << "Unknown exception" << std::endl;
}
```

If no catch function, the `terminate` function is called (terminate calls `abort` function that aborts the program)

Properly written exception safe code employs relatively few `try` blocks

## Throw
- Can throw anything but error types in standard library are typically used
- If a function throws a `const` object, the catch handler argument type must be declared `const` 
- Throw lists are bad practice but you will see them in legacy code
- Exceptions thrown in constructors will cause the destructors to be called for any objects built as part of the object being constructed *before* the exception is thrown
- Don't throw exceptions in a destructor