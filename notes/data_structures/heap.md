# Heap
- Used to keep track of max or min values in a dataset
- **Max-Heap:** Value of root node is the greatest of all the values in the tree
    - Must be true for all sub-trees 
- **Min-Heap** Value of the root node is the smallest of all the values in the tree
    - Must be true for all sub-trees

![Max-min-heap](https://www.geeksforgeeks.org/wp-content/uploads/MinHeapAndMaxHeap.png)

## Implementation
- Binary tree representation is stored as an array 
- Random access to nodes is very efficient compared to pointer traversals through a tree

![Level-order](https://www.geeksforgeeks.org/wp-content/uploads/binaryheap.png)

- Elements are added left to right until an entire level is filled up
    - Leaves no gaps in the array

## Purpose

Useful for:

- Heap Sort- sort an array in $O(nlogn)$ time
- Priority Queues- `insert()`, `delete()`, `extractMax()` and `decreaseKey()` operations in $O(logn)$ time
- Finding the `k`th largest element in an array