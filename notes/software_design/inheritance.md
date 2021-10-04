# Inheritance
- Single Inheritance: occurs when a derived class inherits from only one parent class
- Multiple Inheritance: allows a class to inherit from multiple classes
    - Error prone and should be avoided
- Big 3 are not inherited from a base class by a derived class
    - Assignment operator is *not* inherited from the base class
        - Will be provided with compiler generated one if used and not implemented by the user
- B publicly inheriting A creates the relationship: B is an instance of A
    - private and protected inheritance do not create the same "is a" relationship
  
## Derived Classes
- Have access to base class' public and protected behaviors
    - Protected- used for inheritance. Allows derived class access to something not public

``` c++
class A{

}
class B: protected A {
    // everything public in A becomes protected in B
}

class C: private A {
    // everything public/private in A becomes private in B 
}
```
- Defines new attributes and behaviors
- may override the behaviors of the base class
- intended to be more specific than the base class
- constructor for the base class must be called from the derived class constructor in order to initialzie the base class members in the derived class
    - Non explicitly calling it will result in the default constructor being called implicitly
    - `DerviedClass::DerivedClass(parameters) : BaseClass(parameters) {}` 

- `virtual double func1() const { return 0.0; }` default returns 0.0 
- `virtual void func() const = 0;` forces the derived class to implement the function
    - Example implementation: `void func() const override { //do something }`

## Constructor & Destructor
- When derived class constructor is called
    - 1) Base Class constructor is called to create an instance of the base class (done implicitly or explicitly)
    - 2) Constructor for the derived class is executed
    - Think of an onion (build up dervied object, layer by layer)
- When derived class destructor is called
    - 1) Derived class destructor is executed
    - 2) Base class destructor function is executed
    - Reverse order of ctor, destroy the onion layer by layer

## Overriding
- Dervied version must have same function signature as base version
- Dervied version may include a call to the base version
- Provides more functionality specific to the derived class

## Abstract Class
- A base class that will never have an object instantiated from it
    - Provides a generic interface
- Defined as any class that contains at least one pure virtual function (declare but provide no implementation of)
    - Pure virtual function: `virtual void func() const = 0;` 
    - The equals zero makes the func *pure* virtual instead of just virtual

## Virtual Function
- A function that is expected to be overriden by a derived class
- Incudes full method signature, return type, and may provide default implementation
- Declared in public portion of the class
- Must not be static or a friend of another class
- Pure virtual functions must be overridden
    - If derived class doesn't implement a pure virtual function, the derived class is also an abstract base class
- Non-pure virtual functions can be overidden but do not have to be
- A function defined as virtual in the base class makes it virutal for *all* classes derived from the base class
- Class with virtual functions should contain a virtual destructor
    - Ensures the correct sequence of destructors is called
    - Base class dtor must be virtual
- Should be accessed using pointer or reference of base class type to achieve run time polymorphism

## Why use Virtual Functions?
- Basic inheritance and overriding gives us the expected behavior with concrete instances
- Virtual functions allow us to work with a pointer to the base class
- Virtual functions defined in the base classes permit dynamic binding allowing runtime polymorphism


## Dynamic Binding
- A virtual function invoked using a reference to an objcet
- Allows program to choose appropraite method designed to identify the method for a particular object type at runtime
    - Static binding requires object type to be defined at compile time
- Achieved using vtables

# Polymorphism
- Occurs whens multiple objects from different classes are related by inheritance from the same base class
- Most useful when there are a series of related objects that need to be treated in a uniform manner
- Polymorphic means having many forms 
    - Can have multiple behaviors for the same function depending on the context
- Achieved by using virtual functions and overriding these methods in derived classes
    
## Virtual Function Table
- Created at compile time and put in static memory
- Used at runtime to achieve dynamic binding and runtime polymorphism
- Compiler generates a vtable for each class with at least one method marked as virtual
- Only virtual methods are included in the vtable
- Example vtable for the shape example code from lecture 9:

| Shape Class |   |   |
|---|---|---|
|~Shape   | local or {} | local implementation  |
| area() const   | {} | local implementation |
| volume() const  | {} | local implementation  |
| pShapeName() const | =0 | pure virtual |
| print() const | = 0 | pure virtual |
Shape class is abstract since there are pure virtual methods in the vtable

| Point Class |   |   |
|---|---|---|
|~Point   | local {} | local implementation  |
| area() const   | Shape::area | implementation in shape class |
| volume() const  | Shape::volume | implementation in shape class  |
| pShapeName() const | {} | own implementation |
| print() const | {} | own implementation |
Point class is concrete since there are no pure virtual methods in the vtable

| Circle Class |   |   |
|---|---|---|
|~Circle   | local {} | local implementation  |
| area() const   | {} | local implementation |
| volume() const  | Shape::volume | implementation in shape class  |
| pShapeName() const | {} | local implementation |
| print() const | {} | local implementation |
Point class is concrete since there are no pure virtual methods in the vtable

- When an object of a class containing virtual functions is instantiated, the compiler attaches a pointer to the class's vtable at the front of the object
- Memory and processing costs associated with virtual functions
    - Increased size of object to hold vtable's address
    - Increased compile time to create the vtable for each class with virtual functions
        - More efficient to compute lookup table at compile time rather than determining these relationships at runtime 
    - For each function call, there is an extra step of looking up the address  in the table to the correct implementation
- If marked virtual but not pure virtual, the class will provide its own implementation for it
- Derived class inherits all of the virtual functions from base class
- Polymorphism and use of vtable will be used when the method is marked as virtual and the method is called via a pointer or reference. This means functions in base class with same name will not be hidden like they are when doing override and using concrete instances

## Design Considerations
- Only use inheritance where additional layers of abstraction makes sense
    - Class hierarchies promote code reuse
- Stand alone class --> bsase classes can make refactoring difficult
    - Can create issues with slicing as a result of concrete base classes being able to be instantiated
    - Should make base classes abstract

## Clarifications
- Overloading is creating a method with the same name as an existing method but with different parameters
- Overriding is creating a method in a derived class with the same name and parameters (same signature) as an existing method in its base class
- Polymorphism- ability of different object to be accessed by a common interface
- Polymorphism and overloading are related but not the same 
- Standard hiding of methods of the same name in the base class will occur when the derived class has a concrete instance created
- Dynamic binding and runtime polymorphism occurs when using pointers/references of the base class to point to instances of the derived classes (gives standard interface to access different, but related objects --> definition of polymorphism)
  
![Polymorphism Diagram](https://www.fayewilliams.com/wp-content/uploads/2014/08/polymorphism.gif)