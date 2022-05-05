# Expressions

- fundamental means of specifying computations in a programming language
- unary, binary, ternary indicates number of operands for an operator
- infix vs prefix notation (prefix notation has no precedence concerns or associativity concerns)

## Functional Side Effects:

- functional side effects: when a function changes one of its parametrs or a global variable
- solutions:
    - disallow functional side effects in language definition
    - demand operand evaluation order be fixed
        - ex: java requires operands appear to be evaluated in left-to-right order

## Referential Transparency

- proprty that describes a program if any two expressions in a program that have the same value can be substituuted for one another anywhere in the program, without affecting the action of the program
- opposite of functional side effects