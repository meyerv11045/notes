# Introduction

- Why so many languages? 
  - Evolution- we have learned better ways of doing things over time
  - Special Purposes- many are designed for specific problem domains
  - Diverse Personal Preferences
- What makes a language successful?
  - Ease of use for novice
  - Expressive Power
  - Ease of implementation
  - Wide dissemination at minimal cost 
  - Excellent compilers (possible to quickly compile code to be very small)
  - Backing of a powerful sponsor

## 1.1 Why Study Concepts of Progamming languages?

- Increased capacity to express ideas- diff languages have diff constructs
- Improved background for choosing appropriate languages
- Increased ability to learn new languages by understanding core concepts underyling all languages
- Better understanding of the signifigance of implementation (i.e understanding the choices btw language constructs and their consequences)
- Make it easier to design new languages
- Better use of languages you already know

## 1.2 Programming Domains

- Scientific Applications: large numbers of floating points computations and heavy use of arrays (e.g. Fortran)
- Business Applications: produce reports, use decimal numbers and characters (e.g. Cobol)
- AI: Maniuplate symbols rather than numbers and heavy use of linked lists (e.g. Lisp, Scheme (dialect of Lisp), Prolog)
- Web Software: Collection of different lanugages (markup, general purpose, & scripting)
- Domain Specific Language (DSL)- a language designed specifically to perform tasks in a certain domain 
    - Non-DSL: C, C++, COBOL, Fortran, Java
        - Not small
        - Large expressive power -> not restricted to specific domains
    - DSL: CSS, SQL, UML
        - Can be used by a domain expert who is not necessarily a seasoned programmer
        - Can be created using [Xtext](https://www.eclipse.org/Xtext/) framework or other similar tools
- Fortran was first high level language adopted by many

## 1.3 Language Evaluation Criteria
- Writability: simplciity 
    - Simplicity and Orthogonality
        - orthogonality- a relatively small set of primitive constructs to build the control and data structures of the language
    - Support for Abstraction
    - Expressivity- 
        - a set of relatively convenient ways of specifying operations
        - Strength and number of operators and predefined functions (e.g. Python, Matlab have powerful operators that reduce the amount of code you need to write)
- Readability
    - Simplicity and orthogonality
        - Minimal feature multiplicity (i.e. having more than one way to accomplish a particular operation)
        - Minimal operating overloading
        - Relative small set of primitive constructs
        - Consistent set of rules for combining the primitive constructs
        - Every possible combination is allowed and meaningful
        - Orthogonality means constructs are independent of each other so there are not excpetions to languages rules like arrays of strings are not allowed but all other data types are
        
    - Data Types- adequate predefined data types and structures (e.g. boolean instead of using 0 or 1)
    - Syntax Considerations- 
- Reliability
    - Type Checking at compile or runtime
        - Preventing a bit-pattern representing one type of data from being interpreted as a different type of data
    - Exception Handling to allow taking corrective measures for runtime error
    - Aliasing is the presence of 2+ distinct referencing methods for the same memory location. This is a dangerous, but common, feature
- Cost 
    - Maintaining programs incurrs costs
    - Poor reliability leads to high costs
- Portability 
    - Java code only needs to compile once and the resulting bytecode (instead of machine code) can be run on any OS with a java runtime system installed
    - C++ is not very portable since the code needs to be recompiled for each architecture
- Generality: applicability to wide range of applications
- Well-definedness: the completeness and precision of the language's official definition

## 1.4 Influences on Language Design

- Computer Architecture
  - Imperative Languages- 
    - designed around von Neumann architecture
      - data + programs stored in same memory so instructions and data must be piped to CPU and result piped back to memory (fetch-execute cycle)
    - Central feature is variables that model memory cells, assignment operations which are based on piping operations
    - Very efficient with iteration since instructions are stored adjacently in memory (thus discourages use of recursion for repetition)
  - Functional Languages- 
    - Primary means of computation is applying functions to given parameters
    - Programming can be done without the variables, assignment statements, and iteration used in imperative languages
    - Many benefits though they won't displace imperative languages until a non-von neumann computer is design that allows more efficient execution of programs in functional languages
- Programming Design Methodologies
  - Procedure Oriented (lack of control statements, extensive use of goto statements, incomplete type checking) --> Data Oriented (emphasis on abstract data types to solve problems)  -- > Object Oriented
  - New programming languages in the 70s to support data abstraction
  - OOP developed with the new language Smalltalk that supported it
    - Now OOP is feature of most imperative languages and even some functional languages
  - Main Idea: As new programming design methodoligies evolved, languages evolved with them

## 1.5 Language Categories

1. Imperative 
2. Functional
3. Logic- rule based language where rules are specified in no particular order and the language implementation system chooses the order to apply the rules to produce a result (e.g. Prolog)

## 1.6 Language Design Tradeoffs

- Designing a language requires making criteria tradeoffs (e.g. efficiency for reliability with C not checking for in range indices)
- Conflict between writability and readability is common







