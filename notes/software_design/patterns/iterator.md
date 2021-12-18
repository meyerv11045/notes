# Iterator Pattern 

Also known as cursor 

## Intent

Access elements of a container without exposing its representation

## Applicability
- Require multiple traversal algorithms over a container
- Require a uniform traversal interface over different containers
- When container classes and traversal algorithm must vary independently 


## Structure
![](../static/iterator-pattern.png)

## Participants 

- *Iterator*- defines an interface for accessing and traversing elements
- *ConcreteIterator*- implements the Iterator interface and a specific type of traversal
- *Aggregate*- container interface that defines method for creating an Iterator object
- *ConcreteAggregate*- specific container implementation that implements the create iterator method to return an instance of the correct ConcreteIterator

## Collaborations

- ConcreteIterator keeps track of the current object in the Aggregate and can compute the succeeding object in the traversal

## Consequences

- (+) Flexibility: container and traversal are independent
- (+) Multiple iterators and multiple traversal algorithms
- (-) Additional communication overhead between iterator and container
    - Problematic for iterators in concurrent or distributed systems

## Implementation
- Internval versus external iterators
  - Internal- when the iterator controls the iteration
  - External- when the client controls the iteration (more flexible)
- Violating the object structure's encapsulation
- Robust iterators- ensure insertions/removals won't interfere with traversal 
- Synchronization overhead in multi-threaded programs
- Batching in distributed and concurrent programs

## Related Patterns

- Iterators are often applied to Composite structures