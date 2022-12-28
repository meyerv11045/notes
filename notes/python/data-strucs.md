# Data Structures

## FIFO Queue

- $O(1)$ pop and append from both sides of the queue unlike the standard list which has $O(n)$ append

``` python
from collections import deque

q = deque()

q.append(item)
item = q.popleft()
```



## Priority Queue

- 2nd item in the tuple handles collisions when two keys are equal and item does not implement <
- key is a function

``` python
import heapq

class PriorityQueue:
    def __init__(self, key):
        self.key = key
        self._data = []
        self.idx = 0

    def push(self, item):
        heapq.heappush(self._data, (self.key(item), self.idx, item))
        self.idx += 1

    def pop(self):
        return heapq.heappop(self._data)[2]

    def __len__(self):
        return len(self._data)
```

