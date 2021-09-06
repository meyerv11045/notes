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