# Move Semantics
- makes code faster by adding to code

## rvalue references
- Allow programmers to avoid unnecessary copying and to provide perfect forwarding functions
- Move constructor: `MyClass::MyClass(MyClass&& other);`
    - does not allocate new resources, simply takes the resources from other and sets other to its default ctor state
    - much faster than a copy ctor b/c it doesn't allocate memory and doesn't copy memory buffers
        - only a handful of machine instructions compared to possibly thousands of machine instructions to allocate new memory

- any temp or unnamed variables will be rvalues (determined by compiler)
- assignment of the result of a function is would be 2 copies if move semantics were not used (very costly)
- move ctor is more exception safe than copy ctor 
    - move semantics are safe since we are not grabbing more resources