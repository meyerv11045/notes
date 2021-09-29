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

## Dynamic Binding
- A virtual function invoked using a reference to an objcet
- Allows program to choose appropraite method designed to identify the method for a particular object type at runtime

# Polymorphism
- Occurs whens multiple objects from different classes are related by inheritance from the same base class
- Most useful when there are a series of related objects that need to be trated in a uniform manner
    
## Virtual Function Table
- `vtable` is used in the program to determine which
- Created at compile time and put in static memory
- Used at runtime
- Compiler generates a vtable for each class with at least one method marked as virtual
- Only virtual methods are included in the vtable
- Example vtable for the shape example code from lecture 9:

| Shape Class |   |   |
|---|---|---|
|~Shape   | local {} | compiler default implementation  |
| area() const   | {} | own implementation |
| volume() const  | {} | own implementation  |
| pShapeName() const | =0 | no implementation/pure virtual |
| print() const | = 0 | pure virtual |
Shape class is abstract since there are pure virtual methods in the vtable

| Point Class |   |   |
|---|---|---|
|~Point   | local {} | compiler default implementation  |
| area() const   | Shape::area | implementation in shape class |
| volume() const  | Shape::volume | implementation in shape class  |
| pShapeName() const | {} | own implementation |
| print() const | {} | own implementation |
Point class is concrete since there are no pure virtual methods in the vtable

| Circle Class |   |   |
|---|---|---|
|~Circle   | local {} | compiler default implementation  |
| area() const   | {} | own implementation |
| volume() const  | Shape::volume | implementation in shape class  |
| pShapeName() const | {} | own implementation |
| print() const | {} | own implementation |
Point class is concrete since there are no pure virtual methods in the vtable

- Every instance of a concrete class will allocate a pointer to the class's vtable. 
- Function call involves following two pointers to the correct function implementation
    - Very efficient since all the heavy costs of determining relationships between types is done at compile time and then fast lookups can be done at runtime