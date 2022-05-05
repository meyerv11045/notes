# Ch. 9 Subprograms

- subprogram definition describes the actions represented by the subprogram
- subprograms can either be functions or procedures
    - procedures can modify state
- local variables in subprograms can be stack-dynamic or static
- 3 models of parameter passing: in mode, out mode, and inout mode 
- Some languages allow operator overloading
- Subprograms can be generic 
- A closure is a subprogram and its referencing environment 

## subprogram characteristics

- single entry point
- calling program unit is suspended during execution of called subprogram (i.e. 1 subprogram in execution at any given time)
- control always returns to the caller when the subprogram execution terminates
- *not true for coroutines

## parameters

- positional- binding of actual parameters to formal parameters is by position
    - safe + effective
- Keyword- name of formal parameter to which an acutal parameter is to be bound is specified w/ the actual parameter
    - pro: parameters can appear in any order and avoid param correspondence errors
    - con: users must know the formal parameter's names
- in mode- data is received from the actual parameter
    - pass-by-value- transmit a data value by copying it
    - pass-by-reference- transmit an access path (pointer/reference) to the data value
- out mode- data is returned from the actual parameter
    - pass-by-result- copy value to caller's actual parameter (equivalent of pass-by-value for in mode)
- inout mode- data is transferred in both directions
    - pass-by-value-result (aka pass-by-copy)- combo of by value and by result since we copy in the value at the start and copy it back out at the end
    - pass-by-reference (aka pass-by-sharing)- effiecient passing (no copy) but slower access to extra level of indirection
    - pass-by-name-unevaluated expressions can be passed to formal parameter to be evaluated when the formal parameter is used

## 2 types of subprograms

1. Procedure- expected to produce side effects (can reutrn values only by affecting globals or parameters)
2. Function- expected to reutrn a value and produce no side effects

## local referencing environments

- stack-dynamic local variables
    - (+) support for recursion 
    - (+) storage for local vars is shared among some subprograms
    - (-) allocation/de-allocation and initialization overhead for each call
    - (-) indirect addressing
    - (-) subprograms cannot be history sensitive
- Static local variables have te opposite pros and cons of stack-dynamic local variables

## closure

- a subprogram and the referencing environment where it was defined
- only needed if a subprogram can access variables in nesting scopes and it can be called from anywhere 
    - static-scoped language that doesn't permit nested subprograms doesn't need closures

``` javascript
// anonymous fn returned by makeAdder must be a closure 
function makeAdder(x) {
  return function(y) {return x + y;}
}
```

