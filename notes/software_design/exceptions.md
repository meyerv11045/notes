# Exception Handling
- Purpose: permit the program to catch and handle errors rather than let it occur and suffer the consequences
- Used when system can recover from the error causing the exception
- Exception Handler- recovery procedure
- If no catch function, the `terminate` function is called (terminate calls `abort` function that aborts the program)
- Properly written exception safe code employs relatively few `try` blocks

``` c++
try {
    throw std::overflow_error("overflow error in push")
}
catch (std::overflow_error &excep) {
    // exception handler is here
    std::cout << excep.what() << std::endl;
}
catch (...) {
    std::cout << "Unknown exception" << std::endl;
}
```

## Throw
- Can throw anything but error types in standard library are typically used
- If a function throws a `const` object, the catch handler argument type must be declared `const` 
- Throw lists for functions are bad practice but you will see them in legacy code
- Unwinding the stack refers to when an expection is thrown

``` c++
void func(int x)
{
    char* fizz = new char[1024];
    std::string s("Test");

    if(x) throw std::runtime_error("explosion");

    delete[] test;
}
```
In the above example, memory allocated for `fizz` will be leaked if an exception is thrown b/c `delete[] fizz` is never reached. However, memory allocated for `s` will be properly destructed b/c throwing an exception **unwinds the stack** meaning the destructor will be called on objects in each of the stack frames until a `try catch` block is reached. Since `std::string` has a properly defined destructor, `s` will not create a memory leak when an exception is thrown.

## Constructors & Destructors
- Exceptions thrown in constructors will cause the destructors to be called for any objects built as part of the object being constructed *before* the exception is thrown
- Don't throw exceptions in a destructor