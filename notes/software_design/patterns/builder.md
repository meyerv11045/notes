# Builder Pattern

## Intent
Separate the construction of a complex object from its representation so that the same construction process can create different representations

## Applicability
- Need to isolate knowledge of the creation of a complex object from its part
- Need to allow differrent implementations/interfaces of an object's parts
    - Ex: multiplication in an expression tree can also be represented as repeated addtion 

## Structure
graphical representation of pattern using modified UML notation

Director will command each builder to construct its alternate representation 

Builders have a method the director can call that will return an equivalent product

## Participants
participatnig classes/objects and their responsibilities

## Collaborations
How participants cooperate to carry out their responsibilities

## Consequences
- (+) Can vary a product's internal representation
- (+) Isolates code for construction and representation\
- (+) Finer control over the construction process
- (-) May involve lots of classes

## Implementation
pitfalls, hints, techiques, plus language dependent issues

## Sample Code

## Known Uses
