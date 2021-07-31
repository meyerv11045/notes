#### Heaps:
- Used to maintain a maximum or minimum value in a dataset.
- Commonly used to create a priority queue.
- Heaps tracking the maximum or minimum value are max-heaps or min-heaps. 
- Conceptually, the tree representation is beneficial for understanding. Practically, we implement heaps in a sequential data structure like an array or list for efficiency.
- Think of the min-heap as a binary tree with two qualities:
  - The root is the minimum value of the dataset.
  - Every child’s value is greater than its parent.
  - These two properties are the defining characteristics of the min-heap. By maintaining these two properties, we can efficiently retrieve and update the minimum value.
- As we add elements to the heap, they’re added from left to right until we’ve filled the entire level.
- By filling the tree from left to right; we’re leaving no gaps in the array. The location of each child or parent derives from a formula using the index.
  - left child: (index * 2) + 1
  - right child: (index * 2) + 2
  - parent: (index - 1) / 2 — not used on the root!
- Sometimes you will add an element to the heap that violates the heap’s essential properties.
  - Ex: adding 3 as a left child of 11 in a min-heap which violates the min-heap property that children must be larger or equal to their parent.

- Heapifying- restoring the fundamental heap properties through swapping elements in the tree
  - We’re adding an element to the bottom of the tree and moving upwards, so we’re heapifying up.
- As long as we’ve violated the heap properties, we’ll swap the offending child with its parent until we restore the properties, or until there’s no parent left. If there is no parent left, that element becomes the new root of the tree.