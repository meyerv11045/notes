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
    - 3) **Adaptors**- provide different ways to access sequential and associative containers
        - stack, queue, priority queue
  
### `vector`
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

### `deque`
- Pronounced "deck"
- Double ended queue
- Advantages:
    - Provides efficient index access to data
    - Efficient insertions/deletions at both front and back of queue
        - `push_back()`, `push_front()`, `pop_back()`, `pop_front()`
- Uses a index lookup table to optimize memory and lookup efficiency 
    - Vector will be slightly faster b/c it doesnt need the lookup table due to only pushing back
    - Elements not guaranteeed to be in contiguous storage locations so pointer arithmetic not safe

### `list`
- Implements a doubly linked-list
- Advantages:
    - Const time insertion/removal of elements anywhere in the container
    - Const time moving elements and blocks of elements within the container or even between different containers
        - It just requires pointer assignments instead of copying values and allocating new arrays
- Disadvantages:
    - No support for random-access iterator