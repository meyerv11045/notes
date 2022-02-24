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



## 5.4 Binding

- A binding is an association between an attribute and an entity (e.g. btw a var and its type or val, or btw an operation and a symbol)
- binding time- time at which a binding takes place (can be runtime , compile time, language design time, or language implementation time)

### Binding Attributes to Variables

### Type Binding 

#### Static Type Binding

#### Dynamic Type Binding

### Storage and Lifetime bindings

#### Static Variables

#### Stack-Dynamic Variables

#### Explicit Heap-Dynamic Variables

#### Implicit Heap-Dynamic Variables

## 5.5 Scope







### Lifetime

- storage bindings
    - allocation- getting a cell from pool of available cells
    - deallocation- putting a cell back into the pool
    
    



#### static variables

- bound to memory cells before execution begins and remains bound to the same memory cell throughout execution
- Pros:
    - Direct addressing is very efficient 
    - Globally accessible
    - History sensitive subprogram support 
- Cons:
    - Lack of flexibility (no recursion)
    - No shared storage 

#### stack-dynamic variable

- storage bindings are created for variables when their declaration statements are elaborated (i.e. when the executable code associated with it is executed)
- pros:
    - allows recursion
    - Conserves storage 
- cons:
    - overhead of allocation and deallocation
    - subprograms not history-sensitive since stack vars are deallocated after use
    - indirect addressing is inefficient (go to address of stack pointer and then traverse to correct adress in the stack frame for the variable of interest)

#### explicit heap-dynamic variables

- allocated and deallocated by explicit directives speicfied by the programmer which take effect during execution
    - e.g. using `new` and `delete` to create objects in C++
    - all objects in Java
- Pros:
    - Provides for dynamic storage managemet
- Cons:
    - ineffient indirect addressing
    - unreliable (error prone)
    - complex storage management implementation

#### implicit heap-dynamic variables

- allocation and deallocation caused by assignment statements
- pros:
    - flexibility (generic code)
- Cons:
    - inefficient since all attributes are dnyamic

## Binding:

- Static- binding that first occurs before runtime and remains unchanged throughout program execution
- Dynamic- binding that first occur during execution or can change during program execution 

### Static Type Binding

- explicit declaration: type info supplied in source code (ex: `int x` )
- implicit declaration: type specification through default conventions, rather than explicit declarations
    - ix`mproved writability since we dont need to provide explicit declarations
- type inferencing: form of implicit type declaration
    - static typing without having to declare explicit typees (e.g. `auto`, `var`)



### Dynamic Type Binding

- Variable is bound to a type when it is assigned a value in an assignment statement 
- improved flexibility with generic program units
- high cost due to runtime type checking and interpretation



### searching for nonlocal vars

- search declarations first locally then in increasingly larger enclosing scopes, until one is found for a given name
- static ancestors- enclosing sstatic scopes
- static parent- nearest state ancestor 





static scoping:

- local variables + all variables in all enclosing scopes
- pros:
    - works well for most situations
    - programs easy to read and reason about
- Cons:
    - too much access is possible
    - want vars to be accessed only where needed

dynamic-scoping:

- the local variables + all visible variables in all active subprograms

- references to nonlocal vars are connected to declarations by searching back through the chain of subprogram calls that forced execution to this piint 
- not common in modern PLs except in expection handling 
- pro: convencience
- cons:
    - Poor readability 
    - no static type checking
    - all variables from caller are visisble to called subprogram



types of vars:

- static- bound to mem cells before execution and remains throughout
- stack-dynamic-  bound when declaration statements elaborated
- explicit heap-dynamic- allocated and deallocated by new and delete
- Implicit heap-dynamic- allocation and deallocation caused by assignment statements
- 



