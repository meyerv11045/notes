# Functional Languages

- Lambda expressions describe nameless functions
    - Applied to parameters by placing the parameters after the expression
    - Ex: $(\lambda(x) x * x * x)(2)$ evaluates to 8
- Functional Form
    - Higher order functions
        - lambda expressions are also useful for creating functions to pass as parameters to other functions that expect to receive functions
        - can return other functions
    - Composition of Functions
        - Takes two functions as input and returns a new function that is the result of the 1st function appleid to the second
        - Ex: $h := f \odot g$ which means $h(x) = f(g(x))$
- Inefficient execution on von neumann machines
- simple syntax and semantics
- Programs written in funtional languages can automatically be made concurrent
    - harder to write concurrent imperative languages

## LISP

### History

- Developed in 1958-59 for use in AI 
    - designed @ MIT by John McCarthy
    - Fortran didnt have recursion, the ability to manipulate symbols, and ability to process data in linked lists rather than arrays 
- Base on lambda calculus and mathematical functions
- Interpreted language with garbage collection

### Data Types

- Originally only atoms and lists
- Type is bound at runtime
- names not variables (cant change value of a name after it has been defined)
- list form- parenthesized collection of atoms and/or sublists

### interpretation

- function defintions, function applications, and dataall have the same form 
- `(A, B, C)` can be interpretted differently depending on the context
    - `A` can be a function being called with params `B` and `C`
    - `A` can be a function called on `B` evaluated at `C`

### syntax

- a series of symbolic expressions (or S-expressions)
    - can be an atom or a list 
- an atom can be a number or a symbol
    - a symbol can be a sequence of characters
    - a number can be integers, floats, or ratio of integers (allows us to maintain accuracy with division)
- prefix notation even for simple arithmetic operations 

### grammar

- very simple grammar described by a short EBNF



### lists

- stored internally as singly-linked lists

### semantics

- 1st s-expression in a list is the name of a function
    - Ex: `(foo)` or `(foo a b c)`
- in a function call, all arguments are evaluated first, then the function is applied to the result



### something 

- `#f` is false and `#t` is true 



## lambda expressions

- functions are first-class entities 
- functions can b

### special form function

- `(lambda(x) (* x x))` creates a special lambda function
- can be called by: `((lambda(x) (* x x)) 8)`



## history

- LISP -> Scheme (70s) -> racket 
    - lisp also broke off into a more complex language CommonLisp 
- Scheme
    - cleaner, more modern, and simpler than contemporary dialects of scheme
    - only static scoping 
- order of parameter evaluation doesn't matter since each function has no side-effects
- extensive use of parenthesis makes turning a program text into a parse tree very easy 
    - also no need for operator precedence