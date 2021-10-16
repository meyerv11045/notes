# Queue

Stores data in a first in, first out (FIFO) manner. Basically can be thought of like a line at a store or anywhere.

## Purpose
Queues are great for use where the order of events occur is important

Useful for
- Breadth first search
- Message or print queues
- Simulations with ordered events

## Big O Analysis

The follow operations are due to the linked list implementation

| Operation | Big O |
|-----------|-------|
| push (front/back) | O(1) |
| pop (front/back) | O(1) |
| peek (front/back) | O(1) |

## Code 
``` python
from linked-list import DblyLinkedList

class Queue:
    def __init__(self):
        self.list = DblyLinkedList()
    
    def push_front(self,data):
        self.list.prepend(data)
    def push_back(self,data):
        self.list.append(data)
    def pop_front(self):
        self.list.delete_front()
    def pop_back(self):
        self.list.delete_back()
    def peek_front(self):
        return self.list.head
    def peek_back(self):
        return self.list.tail
```