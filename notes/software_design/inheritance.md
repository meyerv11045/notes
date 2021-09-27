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