# Lambda Functions
- Introduced in C++11
- Create light-weight functions in place
- Designed to replace functors
    - Behind the scenes, the compiler rewrites the lambda to be a functor (so lambdas are just syntax simplification of functors)
- Easy to use with STL

``` c++
std::for_each(int_list, int_list+8, [](int i) {
    std::cout << i << ":";
});
```

## Generic Lambdas
- Introduced in C++14
- Compiler can infer input types
- Allows generic lambdas (since we don't have templates for lambdas)

## Variable Capture
- Can bring in variables from an external scope into the lambda scope
- Can be done by copy or reference
    - Should be done by reference if we want the updated variables outside the scope of the lambda (use by reference to persist state)

``` c++
[int_var, dbl_var] () {
    int i = 7;
    cout << int_var << ' ' << dbl_var << ' ' << i << endl;
} ();
```

## Lambdaas and Member Functions
- Bring `this` into scope, not class member variables
    - Lets you use the class member variables with the implicit `this->`