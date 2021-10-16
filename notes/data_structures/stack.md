# Stack
Stores data in in a last in, first out (LIFO) manner or first in, last out (FILO)

Can be implemented using either an array for when the max size of elements in the stack is known (e.g. deck of cards) or can be implemented using a linked list.
 
## Purpose
Stacks are optimized for adding and removing things from often, where the order of addition and removal plays an important role in solving a certain problem (e.g. matching parentheses)

Useful for:
- Depth First Search
- Backtracking algorithms (e.g. N queens)
- Checking proper brackets/parentheses
- Expression Conversions
- String reversals
- Solving towers of hanoi
- Memory management

### Disadvantages
- Fixed size when implemented as static array
- Slow to grow when implemented as dynamic array
- New/delete operations are slower than array operations for linked list implementation

## Big O Analysis

The follow operations are due to the linked list implementation

| Operation | Big O |
|-----------|-------|
| push | O(1) |
| pop | O(1) |
| peek | O(1) |
 

## Code 
``` python
from linked-list import DblyLinkedList

class Stack:
    def __init__(self):
        self.top = DblyLinkedList()
        self.size = 0
    
    def push(self,data):
        self.top.prepend(data)
    
    def peek(self, data):
        return self.top.head
    
    def pop(self,data):
        self.top.delete_front()
```