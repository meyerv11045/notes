# Bridge Pattern 

## Intent
Separate a logical abstraction interface from its physical implementation(s)

## Applicability
- When interface and implementation should vary independently
- Require a uniform interface to interchangeable class hierarchies

## Structure
![](../static/visitor.png)

## Consequences
- (+) Abstract interface and implementation are independent
- (+) Implementations can vary dynamically (i.e. at runtime)
- (+) Can be used transparently with STL algorithms and containers
- (-) One-size-fits all abstraction and implementor interfaces

## Implementation
- Sharing implementors and reference counting
- Creating the right implementor for the use case (often factories are used)