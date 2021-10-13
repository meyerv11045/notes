# Functors
- Any class that has overriden the parens/function operator `operator()`
    - Allows an instance of the class to be called as a function
- Can do multiple overridings of `operator()` as long as they have different signatures
- Functors are just regular classes
    - Can have constructors & destructores
    - Can have private member variables and functions
    - Can be a template class
- STL algorithms will return a copy of the functor being passed in so that we can access the final state after all iterations

## Functions vs Functors
The below code demonstrates how the same functionality would be implemented differently between just using a function and using a functor

``` c++
void printIt(int i) {
    std::cout << i  << ":";
}

std::for_each(intArray.begin(), intArray.end(), printIt());
std::cout << std::endl;
```

``` c++
class PrintIt {
    public:
    // overloading the parens operator lets us treat an instance of this class as a function
    void operator() (int i) { std::cout << i  << ":"; }
};

// creates instance of PrintIt for each integer in the array and call it as a function
std::for_each(intArray.begin(), intArray.end(), PrintIt());
std::cout << std::endl;
```

## Maintaining State
- Functors allow us to better maintain state through an STL algorithm's iteration compared to regular functions
- Encapsulates the state within a class, preventing pollution of the global namespace with global state variables
- All state is encapsulated in normal class instance lifecycle:

1) Constructor: initial state
2) operator(): state mutation
3) Accessor methods: state querying
4) Destructor: state cleanup (as needed)