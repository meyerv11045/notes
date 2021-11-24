# Visitor Pattern 
any aliases this pattern is known by

## Intent
Centralize operations on an object structure so that they can vary independently but still behave polymorphically

## Applicability
- when classes define many unrelated operations
- when relationships of objects in the structure rarely change, but the operations on them change often
- algorithms keep state that is updated during traversal

## Structure
![](../static/visitor.png)

## Consequences
- (+) Flexibility: visitor algorithm(s) and object structure are independent
- (+) Localized functionality in the visitor subclass instance
- (-) Circular dependency between Visitor and Element interfaces
- (-) Visitor brittle to new ConcreteElement classes

## Implementation
- Double dispatch
- General interface to elements of object structure