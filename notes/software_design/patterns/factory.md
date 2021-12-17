# Factory Method Pattern 
## Intent
Provide an interface for creating an object, but let subclasses decide which class to instantiate.

## Applicability
- When a class cannot anticipate the objects it must create 
- When a class wants its subclasses to specify the objects it creates
- When a standard interface for creating objects is useful in enforcing rules on how objects are created

## Structure
![](../static/factory.png)

## Participants
- Product (ex: Document)
    - defines the interface of objects the factory method cretes
- ConcreteProduct (ex: MyDocument)
    - implements the product interface
- Creator (Ex: Application)
    - declares the factory method which returns an object of type Product (may also provide default implementation that returns a default ConcreteProduct)
    - may call the factory method to create a Product object
- ConcreteCreator (ex: MyApplication)
    - overrides the factory method to return an instance of a ConcreteProduct

## Collaborations
- Creator relies on its subclasses to define the factory method so that it returns the appropriate ConcreteProduct instance

## Consequences
- (+) Client code becomes more flexible since we avoid specifying the class name of the concerete class 
    - Resilient to adding more objects or changing how objects are made
- (+) Client is only dependent on the interface
    - Remove burden of knowing how to create things from the user and give user a simple interface for making new objects
- (-) Construction of objects requires one additional class in some cases

## Implementation
- 2 choices:
    - 1) Creator class is abstract and doesn't implement creation methods meaning it must be subclassed
    - 2) Creator class is concrete and provides a default implementation meaning it can optionally be subclassed
- Can create multiple types of products by parameterizing the factory method
- Should be parameterized if a factory method needs to be able to create different variants

## Known Uses
- All STL containers are factories
- Database connectors (a standard way of creating a database connection that only has to be changed in one place instead of across the application)

## Related Patterns
- Abstract Factory is often implemented with factory methods

# Abstract Factory Pattern

## Intent
Provide an interface for creating families of related or dependent objects without specifying their concrete classes

## Applicability
- When a system should be independent of how its products are created, composed, and represented
- When a system should be configured with one of multiple families of products
- When a family of related product objects is designed to be used together and you need to enforce this constraint
- When you want to provide a class library of products without revealing their implementations

## Structure
![](../static/abstract-factory.png)

## Participants
- AbstractFactory
    - declares an interface for operations that create abstract product objects
- ConcreteFactory
    - implements the operations to create concrete product objects
- Abstract Product
    - declares an interface for a type of product object
- Concrete Product
    - implements the AbstractProduct interface and defines a product object to be created by the corresponding ConcreteFactory
- Client
    - uses only the interfaces defined by AbstractFactory and AbstractProduct classes

## Collaborations
- Normally a single instance of a ConcreteFactory is created at runtime
- AbstractFactory defers creation of product objects to its ConcreteFactory subclasses 

## Consequences
- (+) Flexibility: remove type/subclass dependencies from clients
- (+) Abstraction and semantic checking: hides product's composition
- (-) Hard to extend interface to create new products
 
## Implementation
- Factories are usually best implemented as a singleton
- Parameterization as a way of controlling the interface's size
- Configuration with Prototypes (i.e. determines who creates the factories)
- Essentially groups of factory methods