# Composite Pattern 

## Intent
Compose objects into tree structures to represent part-whole hierarchies. Allows clients to treat individual objects and multiple, recursively-composed objects uniformly.

## Applicability
- Tree structure
- Objects must be composed recursively
- No distinction between individual and composed elements (root node is itself a tree)
- Objects in strcutre can be treated uniformly

## Structure

![Composite Pattern](..static/../../static/composite.png)

## Participants
- *Component*- declares the interface for objects in the composition
  - implements any default behavior common for all classes
  - declares an interface for accessing and managing its child components
- *Leaf*- represents leaf objects in the composition (no children)
- *Composite*- defines behavior for components having children
  - stores child components
  - implements child-related operations

- *Client*- manipulates objects in the composition through the component interface

## Collaborations

- Requests are usually forwarded through composite components to the leaves where the requests are handled.

## Consequences
- (+) Easy to use for the client 
- (+) Easy to add new components
- (-) Overhead: might be prohibitive as the number of objects increases (e.g. impractical for linux kernel with 30+ million lines of code)
- (-) Awkward designs: may need to treat leaves as lobotomized composites

## Implementation
- Do components need to know their parents?
    - If so, add a parent pointer to components
- Does there need to be a uniform interface for both leaves and composites?
- Need to decide who has the responsibility for deleting children
- Do we allocate storage for children in component base class
    - In the expression tree, someone outside the tree will do this actual creation of children nodes (i.e. the interpreter)


## Related Patterns

- Iterator pattern can be used to traverse composites
- Visitor pattern can be used to localize operations/behavior that would otherwise be distributed across composite and leaf classes