# Ch. 2 History of Programming Languages

## 2.3 Fortran

- Environment of development (1954):
    - unreliable computers with small memories
    - focus on scientific applications
    - no programming methodology or tools (writing code in assembly)
    - machine efficiency was most important concern
- Fortran I was released in april of 1957 after 18 years of work
    - code was very fast
    - quickly became widely used
    - programs >400 lines didnt compile correctly due to unreliable machines
- Features:
    - Do loop
    - three-way selection statement: if (expression) negative, zero, positive 
    - user-defined subprograms (no seperate compilation though)
    - only six chars for names
    - no data typing statements (types depended on first letter of name)
- John Backus won 1977 Turing Award for his work on Fortran
- Fortran II came out in 1958 with independent compilation
- Fortran IV came out during 60-62 with explicit type declarations, logical if statements, and subprograms allow passing names as paraemters
    - ANSI standard in 1966 (Fortran 66)
- Fortran 77- character string handling, lgoical loop control statement, if-then-else statement
- Fortran 90 introduced:
    - modules, dynamic arrays, case-statement, pointers, recursion, parameter type checking	
- All Fortran Features:
    - do loop
    - 3 way selection statemenent
    - subprograms
    - logical if statements
    - explicit type declarations
    - character string handling
    - logical loop control statement
    - if else statement
    - modules 
    - dynamic arrays
    - case statements
    - pointers
    - recursion
    - param type checking
  



## 2.5 ALGOL

- Environment of development
    - fortran had barely arrived for IBM 70x
    - many other languages were being developed for specific machines
    - no portable, machie independent languages so Algol was the result of rtrying to design a universal language
- Early Design Process
    - Goals:
      - close to math notation
      - good for describing algorithms
      - must be mechanically translatable to machine code
- Not very succesfful
    - variations such as MAD and JOVIAL (used by air force for 25 years)
    - IBM dropped support
- Algol 58 Features:
    - formalized concept of data types
    - compound staatements
    - else-if clause 
    - parameters seperated by mode (passed in vs. passed out)
- Algol 60 features:
    - subprogram recursion (new for imperative languages)
    - two parameter passing methods (pass by value, by name)
    - nested functions
    - stack storage allocation
- Successes:
    - form base of all following imperative languages
    - first machine-independent language
    - first language with standard syntax (BNF)
- Failures:
    - never widely used
    - lack of IO definition made programs not portable since different machines had different ways of doing IO
    - too flexible making it hard to implement so few compilers implemented the whole language
    - formal syntax definition (BNF) seemed too complex



## 2.8 PL/1

- Development Environment:
    - cocbol and fortran existing
    - by 1963 scientific users wanted more elaborate I/O and business users wanted floats and arrays
- Features
    - unit-level concurrency
    - exception handling
    - recursion toggled on/off for faster execution
    - pointers as a data type
    - cross sections fo arrays
- Successes
    - used in both business and scientifc applications in the 70s
    - subset of language taught in colleges
- Failurse
    - many new features were poorly designed
    - too large and complex

## 2.11 Algol 68

- Design baedon concept of orthogonality
    - a few basic concepts + a few combining mechanisms
- Source of several new ideas
- Features
    - user defined data types
    - dynamic arrays 

## 2.12 Pascal

- Developed by a member of Algol 68 committee
- Simple, Small, and used for teaching from mid 70s to mid 90s
- Easy to use toolkit on any platform
    - provides a compiler that produces p-code so all the user needs to do is write a p-code interpreter in assembly to be able to use Pascal (relatively simpler compared to setting up other languages at the time)
- Features:
    - enumeration types
    - subrange types

## 2.12 C

- Designed for systems programming at bell labs by dennies ritchie and ken thompson
- evolved from BCPL, B, and also ALGOL 68
- Poor type checking but rich set of operators
    - Good for writing systems-level software (OS, etc.)
- Initially spread though UNIX, which included a C compiler
- Bootstrapping:
    - C compilers can be written in c so that only a smaller compiler written in assembly needs to be written to compile the compiler

## 2.15 Smalltalk

- Developed at Xerox PARC in the 70s by Alan Kay
- First full implementation of an OOP language (data abstraction, inheritance, dynamic binding)
- Also pinoreed GUI design



## 2.16 C++

- Developed at Bell labs by Bjarne Srtoustrup in 1980
- Evolved from C and SIMULA67 (where OOP ideas came from)
- Large and complex language because it supports both procedural (backwards support for C code) and OOP 

## 2.17 Java

- Developed at Sun in early 1990s b/c C & C++ were not good for embedded devices
-  Based on C++ 
     - simpler
     - removed unsafe things like pointer arithmetic and left safe thing like references
     - garbage collected memory management
- JVM concept and JIT compilers
- Use increased faster than any previous language due to companies and academics banding together for an alternative from microsoft 