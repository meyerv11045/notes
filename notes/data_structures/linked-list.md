# Linked List

A linked list is basically a data structure that consists of chunks of data that are connected to each other by references to where the next (and possibly previous) chunk is stored in the computer's memory. 

## Purpose
It is optimized for fast insertions/deletions as well as combining and making segments of lists since all of these things are quickly done with simple pointer assignments.

Since linked lists point to different places in memory and require minimal copying of the actual data being stored, linked lists are ideal for storing large pieces of data in a program. For instance, a linked list would be ideal for storing a list of files/images/videos since it does not require actually copying them around when doing operations, it simply just changes the pointers to where they are located in memory.

Linked lists are also useful for implementing other data structures such as stacks, queues, adjacency lists, and sparse matrices.

### Advantages
- Constant time insertions/deletions to/from front and back of list
    - No sihifting elements up or down when insertions/deletions occur
- Constant time splicing of multiple lists since its just pointer assignments
- Dynamic use of memory 
    - Dynamically resizes without any additional copying costs
    - No memory pre-allocated that might go unused
- Efficient way to implement stacks and queues
- Circular linked lists do not have to deal with null pointers

### Disadvantages
- Not stored in contiguous chunk of memory so no random access
    - Direct access to elements via indices is not possible without traversal
- Take up more memory to store than an array due to the pointers
- Traversal is more time consuming compared to an array
- Singly linked list only allow forward traversal
    - Doubly linked lists allow bidirectoional traversal at the cost of an extra back pointer for each node (costly in terms of memory for large lists of millions of nodes)

## Big O Analysis
**Singly Linked List:** with head and tail references

| Operation         | Big O| Explanation                                        |
|-------------------|------|----------------------------------------------------|
| append            | O(1) | just change the tail node pointers                 |
| prepend           | O(1) | just change the head node pointers                 |
| insert (index)    | O(n) | traverse to index and then do pointer assignments  |
| delete front      | O(1) | just change head pointer                           |
| delete back       | O(n) | traverse to 2nd to last node and change pointers   | 
| delete (index)    | O(n) | traverse to index and then change pointers         | 
| traversal (index) | O(n) | follow chain of pointers                           |

**Doubly Linked List:** with head and tail references

| Operation | Big O | Explanation |
|-----------|--------|-------------|
| append | O(1) | just change the tail node pointers |
| prepend | O(1) | just change the head node pointers |
| insert (index) | O(n) | traverse to index and then do pointer assignments |
| delete front | O(1) | just change head pointer |
| delete back | O(1) | just change the end nodes' pointers (makes use of prev pointer) | 
| delete (index) | O(n) | traverse to index and then change pointers |
| traversal (index) | O(n) | follow chain of pointers |

## Code 
**Singly Linked List:**
``` python
class Node:
    def __init__(self, data = None):
        self.data = data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.length = 0


    def append(self,data):
        if (self.head == None):
            self.head = Node(data)
            self.tail = self.head
        else:
            self.tail.next = Node(data)
            self.tail = self.tail.next
       
        self.length += 1

    def prepend(self,data):
        if (self.head == None):
            self.head = Node(data)
            self.tail = self.head
        else:
            temp = Node(data)
            temp.next = self.head
            self.head = temp

        self.length += 1

    def delete_front(self):
        self.head = self.head.next
        self.length -= 1
```

**Doubly Linked List**
``` python
class Node:
    def __init__(self, data = None):
        self.data = data
        self.next = None
        self.prev = None

class DblyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.length = 0
        
    def append(self, data):
        old_tail = self.tail
        old_tail.next = Node(data)
        self.tail = old_tail.next
        self.tail.prev = old_tail

        self.length += 1

    def prepend(self, data):
        new_node = Node(data)
        self.head.prev = new_node
        new_node.next = self.head        
        self.head = new_node

        self.length += 1

    def delete_front(self):
        self.head = self.head.next
        self.head.prev = None

        self.length -= 1

    def delete_back(self):
        new_end = self.tail.prev 
        new_end.next = None
        self.tail = new_end

        self.length -= 1 
```

**Circular Linked List**
Implemented as a doubly linked list but could also be implemented as singly linked list that only uses a tail pointer where tail.next is the head.
``` python
class Node:
    def __init__(self,data=None, next_ = self, prev_ = self):
        self.data = data
        self.next = next_
        self.prev = prev_
    
class CircularLinkedList:
    def __init__(self):
        self.dummy = Node()
        self.length = 0
    
    def append(self,data):
        temp = self.dummy.prev 
        self.dummy.prev = Node(data,self.dummy,temp)
        temp.next = self.dummy.prev
        
        self.length += 1

    def prepend(self,data):
        temp = self.dummy.next
        self.dummy.next = Node(data,temp,self.dummy)
        temp.prev = self.dummy.next

        self.length += 1

    def delete_front(self):
        del_head = self.dummy.next
        self.dummy.next  = del_head.next
        self.dummy.next.prev = self.dummy
        
        self.length -= 1

    def delete_back(self):
        del_tail = self.dummy.prev
        self.dummy.prev = del_tail.prev
        self.dummy.prev.next = self.dummy

        self.length -= 1
```