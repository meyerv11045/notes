# Operator Overloading
- Allows a programmer to define behaviors when built-in operators are applied to user defined types
- `operator<symbol>` is used for the function name of the operator to be overloaded  

``` c++
class String {
public:    
    String &operator=(const String &); // assignment: returns by referenceto allow chaining/compounding assignments
    String operator+(const String &) const; // addition: const method b/c it does not alter the object, but returns a new one
    String operator-() const; // unary negator
...
};
```

``` c++
a = b
// equivalent
a.operator=(b)
```

- Compiler generates default implementation for assignment (=) and address (&) operator
- Overloading an operator does not change:
    - Operator precedence
    - Associativity of the operator (important for unary operator)
    - Arity of the operator (can't turn unary operator into a binary operator or vice versa)
    - Meaning of how the operator works on objects of built-in types


## Friendship
Used for sharing private data members between classes
``` c++
class A{
public:
    int  operator+(const B &rhs) {
        return this->foo + 
    }    
private:
    int foo;
}

class B {
public:
    friend class A; // any object A and all of its functions have access to private members in class B
    friend int A::operator+(const B &rhs); // grants only this method in class A access to private member variables in class B
private:
    int bar;
}

``` 

Implementing an operator function as a non-member function of a class (often used for overloading the insertion/extraction operator):
``` c++
// .h 
class A{
public:
    A(std::string a, std::string b, std::string c);
    friend std::ostream &operator<<(std::ostream &lhs, const A &rhs); // gives method access to the private member variables
private:
    std::string a, b, c;

}
std::ostream &operator<<(std::ostream &lhs, const A &rhs);

// .cpp

A:A(std::string a, std::string b, std::string c): 
    a(a), b(b), c(c) {}

// returns a reference to the ostream that was passed in and modified by adding the data from the rhs object which is not modified in the process
std::ostream &operator<<(std::ostream &lhs, const A &rhs)
{
    lhs << rhs.a << " " << rhs.b << " " << rhs.c <<std::endl;
    return lhs;
}
```