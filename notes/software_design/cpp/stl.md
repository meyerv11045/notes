# Standard Template Library
- Contains generic template classes and functions for containers, iterators, & algorithms
- Allows for development of generic programs that are independent of the underlying container 

## STL Containers
- Are abstract data types (ADTs) that hold data for manipulation
- 3 types
    - 1) **Sequential**- arrange data in a linear manner
        - vector, deque, list
    - 2) **Associative**- maintain data in structures suitable for fast associative operations
        - set, multiset, map, multimap
        - Implemented as balanced binary trees
        - Supports efficient operations on elements using keys ordered by `operator<`
        - Provide efficient, direct accessto store and retrieve elements via a key
        - Keys are maintained in ascending order
    - 3) **Adaptors**- provide different ways to access sequential and associative containers
        - stack, queue, priority queue
  
## `vector`
- Can change size dynamically (resizable array)
- Provides best random-access performance
    - Supports random access iterator
- Insertions/deletions at the back of the vector (`push_back()` and `pop_back()`)
- `push_back`- used when we can only copy
- `emplace_back`- used when we do not need to copy for speed increase
- Pros:
    - Const time access elements by index
    - Linear time iteration over all elements
    - Const amortized (avg) time for adding/removing elements from the end
        - $O(N)/N$
- Cons:
    - consume more memory than arrays due to automatic resizing
- Memory is gauranteed to be contiguous so can use pointer arithmetic

## `deque`
- Pronounced "deck"
- Double ended queue
- Advantages:
    - Provides efficient index access to data
    - Efficient insertions/deletions at both front and back of queue
        - `push_back()`, `push_front()`, `pop_back()`, `pop_front()`
- Uses a index lookup table to optimize memory and lookup efficiency 
    - Vector will be slightly faster b/c it doesnt need the lookup table due to only pushing back
    - Elements not guaranteeed to be in contiguous storage locations so pointer arithmetic not safe

## `list`
- Implements a doubly linked-list
- Advantages:
    - Const time insertion/removal of elements anywhere in the container
    - Const time moving elements and blocks of elements within the container or even between different containers
        - It just requires pointer assignments instead of copying values and allocating new arrays
- Disadvantages:
    - No support for random-access iterator

## `set`
- provides rapid look-up but does not permit duplicates
- $O(logn)$ amortized time complexity for insertion and deletion 
    - Because its stored as a balanced binary tree- usually a red-black tree

``` c++

// Create an output stream iterator with " " as a delimeter
std::ostream_iterator<double> output(std::cout, " ");

std::set<double> doubleSet;

// insert on a set returns a pair: an iterator to the value and T if it was inserted, F if it already existed
std::pair<std::set<double>::const_iterator, bool> pairValue;
pairValue = doubleSet.insert(13.2)

// or simply use auto to infer the type
auto pairValue = doubleSet.insert(13.2)

std::cout << *(pairValue.first) << (pairValue.second ? "was" : "was not") << "inserted" << std::endl;
std::cout << "Set contains: ";
std::copy(doubleSet.begin(),doubleSet.end(),output);
```

### `multiset`
- provides rapid look-up but permits duplicates
- Order of data determined by a comparator function

``` c++
std::multiset<int> intMultiSet;

// insert on a multiset just returns an iterator
intMultiSet.insert(1);

// check for an item
if (intMultiSet.find(2) == intMultiSet.end())
    std::cout << "Not found"
```

## `map`
- Provides lookup using a rapid key based lookup
- Each value is associated with a unique key (no duplicate keys)
- AKA associative array
- Implemented as either a hashtable or red-black tree depending on the compiler

## `multimap` 
- Allows duplicate keys
- No index operator notation since ambiguity in which key is being referred to


## STL Algorithms
- Operate over iterators, not containers
- Composing an algorithm with a container by invoking the algorithm with the iterators for that container
- Templates provide compile-time type safety when combining containers, iterators, algorithms
- Primary categories:
    - **Non-mutating**
    - **Mutating**
    - **Sorting and Sets**: sort or search ranges of elements and act on sorted ranges by testing values
        - Ex: `sort()`, `nth_element()`, `binary_search()`
    - **Numeric**: produce generally numeric results
        - Ex: `min()` `min_element()`, `next_permutation()`

## Mutating
- `Remove` packs all the valid elements to the front of the container
    - Doesn't actually remove the element
    - Must be followed by a container specific call to actually remove the element and change the size of the container
- Generate calls the passed in function to create a new value and then puts it into the container (does this for a range)
    - generate_n does this n times instead of for a range
- remove

- `transform()` is an important and commonly used algo
    - takes from one domain to another domain
    - applies a function (takes in type of input container and returns type of output container) to elements int the input container and adds them to an output container
    - expects there to be space in the output container (space must be preallocated which can be done since its a 1:1 mapping from the input container to the output container)
        - many algorithms we don't know the output of so we cant presize/preallocate
        - `back_inserter` is a adaptor that grows the size of the container by calling `push_back` (more flexible in that we don't need to presize anything)
    - corresponds to MapReduce

    - another version has a function that takes two inputs and returns 1 output to write back to the same input container

    - understand 4 and 5 parameter versions
    - bind prob not on quiz

### random notes
- boolean/predicate function- returns T/F based on a condition. usually passed to STL algorithms such as `find_if()`
- `sort()` is performed inplace. can pass a different operator than < for the comparator
- erase is just doing smush copying (behavior is not what you would expect)