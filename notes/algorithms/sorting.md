# Sorting Algorithms

- General Sorting algorithms on abstract data types where the only operation you can perform is a comparison provably have a lower bound of $O(n \log n)$ 
    - this means there are no faster sorting algorithms than $O(n \log n)$ except for in the unique case of sorting integers in which case we can do more than comparisons in order to get the sort down to linear time
    - the proof follows from the gauranteed height of a decision tree for sorting the elements (see the MIT 6.006 lecture 7 video for an intuition)

## Heap Sort 

- Time: $O(n \log n)$
- Space: $O(1)$ 

### Algorithm w/ Max-Heap

1. Build max heap from unordered array
2. Find maximum element $A[1]$
3. Swap elements $A[n]$ and $A[1]$ 
    - now max element is at the end of the array 
4. Discard node $n$ from the heap by decrementing the heap-size variable
5. New root may violate max heap property, but its children are max heaps. Run max heapify to fix this 
6. Goto step 2 unless the heap is empty 

### Algorithm w/ Min-Heap

1. Build min-heap from unordered array $O(n)$
2. Select and remove root $O(1)$
3. Fix heap $O(\log n)$ 
    - Can't make assumptions about rest of tree like in build heap
4. Repeat 2,3 $n$ times to give runtime $O(n \log n)$

## Quick Sort

- Avg Time: $O(n \log n)$
    - Worst Case is $O(n^2)$
- Space: $O(1)$
- Divide and Conquer (in place)
- [HackerRank Video](https://www.youtube.com/watch?v=SLauY6PpjW4)

1. Select a pivot value from the array 
2. Using left and right indices starting from the edges, swap elements out of order (every element < pivot should be before every element > pivot)
3. return the partition point (the point where the elements < pivot and > pivot meet)
4. call quicksort recursively on the two halves of defined by the partition point

- Can choose *pivot* in many ways (e.g. median/middle of array)
    - how you choose your pivot is main thing that affects runtime

```python
def quicksort(A, left, right):
	if (left < right):
    pivot = A[left + (right-left) / 2]
    index = partition(A, left, right, pivot)
    
    quicksort(A, left, index - 1)
    quicksort(A, index, right)

def partition(A, left, right, pivot):
  while (left <= right):
    
    while (A[left] < pivot):
      left += 1
    while (A[right] > pivot):
      right -= 1
  	
    if (left <= right):
      swap(A, left, right)
      left += 1
      right -= 1
 	return left 
```

## Merge Sort

- Time: $O(n \log n)$
- Space: $O(n)$
- Divide & Conquer
- [HackerRank Video](https://www.youtube.com/watch?v=KF2j-9iSf4Q)
- Split the array into halves until you reach a base case of 2, sort the base case, then combine the sorted subproblems in sorted order to create the final sorted array

## Bubble Sort

- Time: $O(n^2)$
- Space: $O(1)$
- [HackerRank Video](https://www.youtube.com/watch?v=6Gv8vg0kcHc)
- "bubbles" the largest elements to the end of the array
    - inefficient since each iteration of $n$ comparisons only finishes sorting 1 element

- only time this might be useful is if the array is mostly sorted

``` python
def bubblesort(A):
  is_sorted = False
  last_unsorted = len(A) - 1
  while not is_sorted:
    is_sorted = True
    for i in range(last_unsorted):
      if (A[i] > A[i+1]):
        swap(A, i, i+1)
        is_sorted = False
   	last_unsorted -= 1
```

## Linear-Time Sorting

- More accurately Integer Sorting
    - major area of reserach 
- Assume $n$ keys being sorted are integers in a range (0, ..., k-1) and each fits in a word of memory 
    - Since we are working with only integers, we can do more than just comparisons in order to speed up the sort
- [MIT 6.006 Lecture Video](https://www.youtube.com/watch?v=Nz1KZXbghj8&list=PLUl4u3cNGP61Oq3tWYp6V_F-5jb5L2iHb&index=7)

### Counting/Bucket Sort

- Performs no comparisons 
- Uses knowledge of the range with upper bound of $k$
- Counts number of occurences of each element in the range (0 to k)
- Then in the output array, it will merely make sure there are the correct number of occurences for each element in the range and the frequency array is traversed in order to produce the sort 
- A more generalized version is seen below where the items can be any data structure, as long as they have an integer key 
    - this version will make sure all of the item's data is moved during the sort

``` python
L = array of k empty lists
# O(n)
for j in range(n):
  L[key(A[j])].append(A[j]) # O(1)
 
output = []
# O(n + k)
for i in range(k):
  output.extend(L[i]) #O (|L| + 1)
```

- Overall runtime: $O(n + k)$
    - If $k$ is order $n$, then the runtime is linear

### Radix Sort

- Uses counting sort as a subroutine
- Performs in linear time even for $k$ polynomial in $n$ (e.g. $k \in O(n^{100})$)
- Imagine each integer as base $b$ (e.g. in the form of its digits)
    - \# digits: $d = \log_b k$
- Sort the integers by least significant digit
    - repeat $d$ times (up to sorting by the most significant digit)
    - Sort by digit using counting/bucket sort $O(n + b)$
        - all digits are between 0 and $b - 1$
        - we can compute the digits in constant time (no need to actually convert them to base $b$) using modulo and other operators
- So the total time is $O(d(n+b))$
    - We substitute value of $d$ from above to get $O(\log_b k (n + b))$
    - We want to choose a $b$ to minimize the runtime 
        - minimized when $b = \Theta(n)$
        - $O(n \log_n k )$
- If $k \leq n^c$ then $O(nc)$
    - If integers are reasonably small in value (polynomial in $n$), then we get a linear time sorting algorithm



## Bucket Sort

- Create buckets (e.g. array/linked list) for each element in the range of your data
    - IMPORTANT: need to know the range of your data before applying this sorting technique
    - Buckets must be accesible in $O(1)$ time
- Create a function that is a bijection betwen different element types and the bucket indices
    - function that maps everything to its own bucket with no crashes (e.g. temperature data mapped to a bucket)
- Place each element in its bucket
- "Collect" all of the buckets
- Runtime:
    - often considered $O(n)$
    - more specific: $O(n + k)$ 
    - $n$- number of elements 
    - $k$- number of buckets/range of the input 
        - If $k$ is linear in $n$ then $O(n)$ runtime
        - Otherwise the running time will be $O(k)$ 
- When not to use:
    - Ex: sorting integers in range 1 to 10,000,000 but only sorting 100 numbers
        - Bucket sort takes $10^7$ to collect all the buckets
        - Mergesort would take ~665 comparisons

## Radix Sort

- Radix means base 
- many descriptions:
    - read digits left to right, right to left
    - divide and conquer with recursive calls
- Runtime
    - $n$- number of elements
    - $\ell$ - length of elements
    - $k$- upper bound on range of digits
    - Each sort is a bucket sort of $n$ items into $k$ buckets $O(n + k)$
    - There are $\ell$ sorts to be done
    - $O(\ell (n + k))$
