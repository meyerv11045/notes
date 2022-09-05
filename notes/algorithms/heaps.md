

# Priority Queue

- ADT that implements a set $S$ of elements, each element associated with a key

## Operations

- `insert(S,x)`: insert element x into set S
- `max(S)`: return element of $S$ with largest key
- `extract_max(S)`: return element of $S$ with largest key and remove it from $S$
- `increase_key(S,x,k)`: increase value of $x$'s key by $k$

# Binary Heap

- Implementation of a priority queue
- An array visualized as a nearly complete binary tree
    - all leaves are at max depth or max depth -1
    - every leaf has 0 or 1 sibling
    - Array has benefit of $O(1)$ random access for getting children
- Calculating node indices (1-indexed):
    - root $i =1$
    - parent($i$) = $i / 2$
    - left($i$) = $2i$
    - right($i$) = $2i + 1$
- Max-Heap Property- The key of a node is $\geq$ the keys of its children
    - `max(S)` is trivial
    - `extract_max(S)` is not trivial

## Operations

- `build_max_heap(A)`: produces a max heap from an unordered array

    ``` python
    def build_max_heap(A):
    	for i in range(n/2, 0, -1): #n/2 to 1
    		max_heapify(A, i)
    ```

    - Why start at n/2?
        - Elements $n/2 + 1$ to the end of the array are leaves
        - So we build up max-heap from leaves
    - Runtime of $O(n)$
        - only 1 node with $O(\log n)$ runtime (the root),
        - the lowest level with the most nodes, has the smallest number of operations
        - detailed analysis:
            - `max_heapify` takes $O(1)$for nodes that are one level above the leaves
            - `max_heapify` takes $O(\ell)$ time for nodes that are $\ell$ levels above the leaves
            - $n/4$ nodes w/ level 1, $n / 8$ nodes with level 2, .... , 1 node $\log n$ level
            - Total amount of work in the for loop:
                - $n/4 (1c) + n/8 (2 c) + n / 16 (3 c) + \cdots + 1 (\log n c)$
                - let $n/4 = 2^k$
                - $c 2^k( 1/2^0 + 2/2^1 + 3/2^2 + \cdots (k+1)/2^k)$
                    - the series $\sum_{i=0}^k \frac{i + 1}{2^i}$ is bounded by a constant
                - Therefore, we have $\Theta (n)$ time complexity

- `max_heapify(A,i)`: correct a single violation of the heap property in a subtree's root

    - assume that the trees rooted at left($i$) and right($i$) are max heaps
    - If element $A[i]$ violates the max-heap property, correct the violation by trickling it down the tree, in order to make the subtree rooted at $i$ a max-heap

        - Exchange bigger child with $A[i]$
        - Recursively call max heapify on the subtree where the original parent is now the root
    - This operation runs in $O(\log n)$

        - algorithm runs level by level on a height constrained tree -> produces logarithmic time complexity

```python
def max_heapify(A,i):
	l = left(i)
	r = right(i)

	if (l <= heap-size(A) and A[l] > A[i]):
		largest = l
	else:
		largest = i

  if (r <= heap-size(A) and A[r] > A[largest]):
    largest = r
  if (largest != i):
    swap(A[i],A[largest])
    max_heapify(A, largest)
```

## Types of Heaps

- Binary Heap
    - Min-Heap
    - Max-Heap
- $d$-ary heap- every node has 0 up to $d$ children
- Fibonnaci Heap- collection of trees
- Binomial Heap: priority queues that can be easily merged together

## Resources

- [MIT 6.006 Lecture](https://www.youtube.com/watch?v=B7hVxCmfPtM), [MIT 6.006 Notes](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/lecture-videos/MIT6_006F11_lec04.pdf)