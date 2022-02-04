# Basic Graph Algorthims

## Graph Representation

A graph is a set of vertices and edges $G = (V, E)$

### Adjacency List

- Array of length $|V|$ with each array value being a linked list of neighboring nodes 
- Common choice b/c its a compact way to represent sparse graphs ($|E| < |V|^2$)
- Can represent a weighted graph by using a weight function to compute the weight and store it in the linked list node for neighboring vertices (also can use another array and linked list, it really depends on language and implementation details)
- Cons: no quicker way to determine whether an edge is present in the graph than to search for the 2nd vertex in the first vertex's linked list of neighbors

### Adjacency Matrix

- 2D array/matrix of size $|V| * |V|$
- Good choice when graph is dense ($|E| \approx |V|^2$)
- Good choice when we need to quickly know if an edge connects to vertices ($O(1)$) due to random-access property of arrays/matrices)
  - Comes at the cost of higher space complexity than adjacency list ($\Theta(V^2)$ memory)
- Can represent a weighted graph by using weights instead of just 0 and 1
- In an undirected graph, the adjacency matrix $A = A^T$ so in very large graphs it can be more space efficient to only store entries above or below the diagonal (saves half the memory)
- Simpler so they are sometimes preferred in cases where $V$ is known to be small

## Breadth First Search

- Given graph $G = (V,E)$ and source vertex $s$
- Explores edges of G to visit every vertex reachable from $s$
- Computes the distance (smallest # of edges) to from $s$ to each vertex
- Explores all edges at depth $k$ before exploring any edges at depth $k + 1$
- Marks explored vertices as visited so they are not reexplored

### Analysis

- Enqueing and dequeing take $O(1)$ time
- All nodes are added to the queue when exploring the entire graph so this takes $O(V)$ time (overhead for initialization)
- Once a vertex is dequeued, its entire adjacency linked list is scanned (adding vertices to the queue that have not been visited) 
  - Since all the adjacency lists must be scanned in their entirety, it takes $\Theta(E)$ time
  - We explore all edges $\Theta(E))$
    - each edge explored once in undirected graph
    - each edge explored twice in directed graph
- Total runtime is $O(V + E)$ linear to the size of the adjacency list of $G$

## Edge Classification

- tree edge
- backward edge
- forward edge

## Connectivity 

There is a path from each vertex to every other vertex

### Directed Graph

- Strongly Connected
- Strongly connected components or strong components
- An SCC is a set of vertices such that there is a path from every vertex to every other vertex in the set

### Undirected Graph

- Connected- run DFS or BFS and see you visit all the nodes (keep a count and compare to size of graph)
- Connected Components
- Articulation Points- every path btw v and w contains a, then a is an articulation point OR removing a  splits G into two or more parts 
- Biconnected Components- no articulation points in the graph  

### Finding Strongly Connected Components on Directed Graphs

1. Perform DFS (from random start vertex), when a vertex is finished (colored black) push onto a stack
2. Compute the transpose of the graph (flip direction of edges)
3. Run DFS on $G^T$, with the starting vertex being the top of the stack
   - When you get stuck, pop from the stack to restart DFS with a new start ppint 
4. Each tree in the DFS forest of $G^T$ is a strongly connected component 

- Why does this work?
- This algorithm doesn't apply to undirected graphs

### Finding Articulation Points on Undirected Graphs

































