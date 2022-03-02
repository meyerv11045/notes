# Ch. 5

## 5.3 Variables

- Variable is a sextuple of attributes 
    - name, address, type, value, lifetime, scope 

### Names

- most PLs are case senstive (C based languages)
    - reduces readability but following naming conventions fixes this mostly
- some are case insensitive (Ada, Fortran, Pascal, SQL)
- Semantically meaningful capitalization sometimes exists (e.g. Go using capitals to access members of packages)
- reserved word- special word that can't be used in user-defined names
    - None: PL/1
    - Many: COBOL
- keyword- special only in certain contexts

### Address 

- memory address a var is associated with
- var may have diff addresses at diff times during execution
- Referred to as the L-value of a variable by compiler writers
- Aliases- 2+ vars refer to same memory address
    - hinders readability 


### Type

- Determines:
    - the range of values of variables 
    - the set of operations defined for values of that type 

### Value

- The contents of the memory location 
- Referred to as the r-value of a variable 



## 5.4 Binding Attributes to Variables

- A binding is an association between an attribute and an entity (e.g. btw a var and its type or val, or btw an operation and a symbol)
- binding time- time at which a binding takes place (can be runtime , compile time, language design time, or language implementation time)
- Static Binding- bindings that first occur before runtime *and* remain unchanged throughout execution
- Dynamic Binding- bindings that first occur during execution *or* can change during execution of the program

### Type Binding

#### Static Type Binding

- Explicit Declaration- type information supplied in source code (e.g. statically typed languages like C, Java)
- Implicit Declaration- type specification through default conventions (e.g. FORTRAN, Perl)
    - Type Inferencing- static typing without having to declare explciti types (e.g. use of `auto` in C++ will have compiler infer the type)

#### Dynamic Type Binding

- Variable is bound to a type when its assigned a value in an assignment statement 
- Increased flexibility
- High cost of runt-time type checking and interpretation
- JavaScript, Lisp, Python, PHP, matlab

### Storage and Lifetime Bindings

#### Static Variables

- bound to memory cells *before execution begins* and remains bound to same memory cell *throughout execution*
- Pros:
    - Direct addressing is very efficient 
    - Globally accessible
    - History sensitive subprogram support 
- Cons:
    - Lack of flexibility (no recursion)
    - No shared storage 

#### Stack-Dynamic Variables

- Storage bindings created for variables when their declaration statements are elaborated (i.e. executed)
- pros:
    - allows recursion
    - Conserves storage 
- cons:
    - overhead of allocation and deallocation
    - subprograms not history-sensitive since stack vars are deallocated after use
    - indirect addressing is inefficient (go to address of stack pointer and then traverse to correct adress in the stack frame for the variable of interest)

#### Explicit Heap-Dynamic Variables

- Allocated and deallocated by explicit directives from the programmer (take effect during execution)

- Dynamic objects in C++ via `new` and `delete`, all objects in Java

- Pros:

    - Provides for dynamic storage managemet

- Cons:

    - ineffient indirect addressing
    - unreliable (error prone)
    - complex storage management implementation

    

#### Implicit Heap-Dynamic Variables

- allocation and deallocation caused by assignment statements
- all variables in lis; all strings/arrays in JS, Perl, & PHP
- pros:
    - flexibility (generic code)
- cons:
    - inefficient since all attributes are dnyamic

#### Lifetime

- storage bindings
    - allocation- getting a cell from pool of available cells
    - deallocation- putting a cell back into the pool

#### Types of Variables Summary

- **static**- bound to mem cells before execution and remains throughout
- **stack-dynamic**-  bound when declaration statements elaborated
- **explicit heap-dynamic**- allocated and deallocated by new and delete
- **implicit heap-dynamic**- allocation and deallocation caused by assignment statements



## 5.5 Scope

### Static Scope

- based on program text
- referencing environment:  local variables + all variables in all enclosing scopes
- aka Lexical Scope
- Finding nonlocal variables- search declarations in increasingly larger enclosing scopes until one is found for the given name
- Static Ancestors- enclosing static scopes
    - Static Parent- nearest static ancestor 
- pros:
    - works well for most situations
    - programs easy to read and reason about
- Cons:
    - too much access is possible
    - want variables to be accessed only where needed
    - as a program evolves, initial structure is destroyed (local vars tend towards being global variables)

### Dynamic Scope

- based on calling sequences of program units
- referencing environemnt: the local variables + all visible variables in all active subprograms
- Finding nonlocal variables- search declarations back through the chain of subprogram calls 
- Not used in modern PLs except for exception handling 
- Pros: convenience since the called subprogram is executed in the context of the caller
- Cons: 
    - poor readability
    - no static type checking (must be done dynamically)
    - all variables from caller are visible to called subprogram
