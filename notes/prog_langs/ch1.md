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
    - Syntax Considerations
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
    - Imperative Languages
      - designed around von Neumann architecture
        - data + programs stored in same memory so instructions and data must be piped to CPU and result piped back to memory (fetch-execute cycle)
        - new paradigm of storing the program in the computer (stored-program computer)
      - Central feature is variables that model memory cells, assignment operations which are based on piping operations
      - Very efficient with iteration since instructions are stored adjacently in memory (thus discourages use of recursion for repetition)
    - Functional Languages
      - Primary means of computation is applying functions to given parameters
      - Programming can be done without the variables, assignment statements, and iteration used in imperative languages
      - Many benefits though they won't displace imperative languages until a non-von neumann computer is design that allows more efficient execution of programs in functional languages
- Programming Design Methodologies
      - Influences:
        - 50s and early 60s: simple applications
          - worry about machine efficiency
        - late 60s: people efficiency is became more important
          - strucuted programming; top-down design and step-wise refinement (refining code in steps)
        - late 70s: process-orientied to data-oriented
          - data abstraction
        - middle 80s: object-oriented programming
          - data abstraction + inheritance + polymorphism
      
      - Procedure Oriented (lack of control statements, extensive use of goto statements, incomplete type checking) --> Data Oriented (emphasis on abstract data types to solve problems)  -- > Object Oriented
      - New programming languages in the 70s to support data abstraction
      - OOP developed with the new language Smalltalk that supported it
        - Now OOP is feature of most imperative languages and even some functional languages
      - Main Idea: As new programming design methodoligies evolved, languages evolved with them
  

## 1.5 Language Categories

1. Imperative- variables, assignment statements, iteration (includes OOP languages and scripting languages) 
2. Functional- applying functions to given parameters (purest form is mathematical and has no memory, time, or state)
3. Logic- rule based language where rules are specified in no particular order and the language implementation system chooses the order to apply the rules to produce a result (e.g. Prolog)
    - program statements describe facts and rules
    - computer's job is to construct a proof based on the given facts + rules

## 1.6 Language Design Tradeoffs

- Designing a language requires making criteria tradeoffs (e.g. efficiency for reliability with C not checking for in range indices)
- Conflict between writability and readability is common
- Reliability vs Cost of Execution

## 1.7 Implementation Methods

1. Compilation- programs are translated into machine language  

      - Slow translation, fast execution when compared to interpretation 
      - Translation only occurs once, but program is executed many times
      - Several Steps 
        - Lexical Anlaysis- converts characters in source program into lexical units
        - Syntax Analysis- transforms lexical units into parse tree and check syntactic correctness
        - Semantics Analysis- type checking and intermediate code generation (often in an assembly like language)
        - Code Generation- machine code generated 
2. Pure Interpretation- programs are interpreted

      - No translation into machine language, code is executed on the fly
      - Rare for traditional high-level languages
      - Pros:
        - Execution is immediate 
        - Easier implementation of debugging programs (altough errors are not found until actually executed)
      - Cons: 
        - 10 to 100 times slower execution than compiled programs
        - Often requires more space
3. Hybrid-high-level language translated to an intermediate language

      - Translation can catch many errors early
      - Interpeting much simpler byte code --> faster runtime
      - Faster than pure interpretation 
      - Ex: Java compiles to intermediate byte code that is machine independent so it can be run on any machine with a run-time system (JVM)
4. Just-in-Time Compilation (aka Dynamic Compilation): 

      - Method for improving the performance of interpreted programs
      - During execution of the program, parts of the program that are used frequently may be compiled into native code to improve performance
        - Ex: with java, the JVM runs the bytecode, but for certain functions that might be heavily used, they are compiled into machine code for the specific machine to increase performance 
      - Intermediate language (bytecode) methods are translated into machine code when they become hot (i.e. executed more often than a threshold)
        - The machine code is then kept for subsequent calls
      - Compile commonly used parts of program to machine code (e.g. Java, Matlab, .Net languages)
        - Attempts to get the benefits of both an interpret and compiled program
      - Java and C# have runtime environments (JVM, CLR) that can profile a program while it is being run to allow for more optimized code to be generated
      - Many JIT compilers only compile the code paths frequently used to limit overhead of compilation during runtime







