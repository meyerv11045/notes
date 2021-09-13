# C++ Compiler
4 Steps:
1. Preprocessor: deletes comments, expands macros (anything with `#` prefix), replace file includes and constants with the values
      - `#include` brings in lots of files to create a larger temp file with everything needed
      - Summary: Pull together all needed code
2. Compiler: takes the code and produces architecture dependent assembly code (type, syntax, grammar rules are applied here)
3. Assembler: takes the assembly code and translates it to machine code
      - No commnon errors at this step
4. Linker: takes all seperate translation units and tries to link them together
      - Common Errors: symbol missing (declare and call a method but never define it), couldn't open output file (tried to build while debugger was running on the old executable)

- Clang and Gcc compiler will be used. 
- Undefined behaviors are different between C++ compilers

## Command Line Arguments
``` c++
int main(int argc, char **argv) {

}
```
`argc` is the number of command line arguments (strings)
`**argv` is a pointer to an array (a pointer) containing pointers to the command line strings

Always one argument (the name of your program itself) 

When running a program the OS loader finds the executable on disk and passes in any additional arguments from the command line to the main function

## Explicit vs. Automatic Conversions
A single argument constructor provides the aiblity to convert the value of the argument to the clas type.


implicit conversion converts the statement to a 

``` c++
Class A {
public:
      A();
      A(int);
      A(const char*, int=0);
}

// implicit conversion:
A c = 1; // same as A c = A(1)
A c = "someword" // same as A c = A("someword")
```

``` c++
Class A {
public:
      A();
      // don't need to give params names in the header but its helpful, only required in the cpp implementation
      explicit A(int);
      explicit A(const char*, int=0);
}

// implicit conversion no longer allowed
A c = 1; // will now throw compiler errors
A c = "someword" // same as A c = A("someword")

// allows:
A a1;
A a2 = A(1);
A a3(1);
A a4 = A("Test");
A a6 = static_cast<A>(1);
A* p = new A(1);
```

## Reference
- Another name for an existing object
- Not a pointer and doesn't behave like a pointer
- 3 Major differences from a pointer:
    - 1) No null references
    - 2) All references require initialization when they are declared
    - 3) A reference always refers to the object with which it is initialized (cannot be made to refer to a different object later)

### References and Const
- reference to a non const cannot be initialized with a literal or temporary value 
- a refernce to a const can be initialized with a literal or a temporary value
``` c++
double &cd = 12.3; // error!
const double &cd = 12.3; //no error
```

## Function Calls:
- 1) Pass by value: calls copy constructor
- 2) Pass by pointer
    - Function call must send address of the variable: `f(&<var-name>)`
    - Function def must use `*` to create an alias for the variable: `<return-type> f(<data-type>* <var-name>) { ... }`
``` c++
int test(char* letter) {
      return int(*letter)
}

char testLetter = 'a';
std::cout << test(&testLetter) << std::endl; // prints a
```
- 3) Pass by reference: allow

types not matching causes attempt to implicitly cast to the correct type which effectively causes a copy call when making a temp copy

therefore, types have to match


## Debugger
- Can set breakpoints to run the program until a certain line
- Can set watch points to run the program until a certain condition
- LLVM/GDB debuggers can be used from the terminal