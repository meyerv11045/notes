# Exception Handling
- Purpose: permit the program to catch and handle errors rather than let it occur and suffer the consequences
- Used when system can recover from the error causing the exception
- Exception Handler- Recovery procedure

``` c++
try {
    throw Exception("Something went wrong");
}
catch () {

}
```

If no catch function, the `terminate` function is called (terminate calls `abort` function that aborts the program)

Properly written exception safe code employs relatively few `try` blocks

## Throw
- Can throw anything but error types in standard library are typically used
- If a function throws a `const` object, the catch handler argument type must be declared `const` 