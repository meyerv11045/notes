# Graph Representation

A graph is a set of vertices and edges $G = (V, E)$

## Adjacency List

- Array of length $|V|$ with each array value being a linked list of neighboring nodes 
- Common choice b/c its a compact way to represent sparse graphs ($|E| < |V|^2$)
- Can represent a weighted graph by using a weight function to compute the weight and store it in the linked list node for neighboring vertices (also can use another array and linked list, it really depends on language and implementation details)
- Cons: no quicker way to determine whether an edge is present in the graph than to search for the 2nd vertex in the first vertex's linked list of neighbors
- Takes $O(V + E)$ to build

## Adjacency Matrix

- 2D array/matrix of size $|V| * |V|$
- Good choice when graph is dense ($|E| \approx |V|^2$)
- Good choice when we need to quickly know if an edge connects to vertices ($O(1)$) due to random-access property of arrays/matrices)
  - Comes at the cost of higher space complexity than adjacency list ($\Theta(V^2)$ memory)
- Can represent a weighted graph by using weights instead of just 0 and 1
- In an undirected graph, the adjacency matrix $A = A^T$ so in very large graphs it can be more space efficient to only store entries above or below the diagonal (saves half the memory)
- Simpler so they are sometimes preferred in cases where $V$ is known to be small

## Runtimes 

- Building a graph:
    - adjacency list: $O(V + E)$
    - adjacency matrix: $O(V^2)$ 
- Finding vertex $x$ in an array or matrix using its id: $O(1)$ 
- Determine number of vertices or edges in graph: $O(1)$
    - assume information is recorded when graph was input
- Explore all neighbors of vertex $x$: $O(V)$
- Explore all neighbors of all vertices in the graph:
    - adjacency list: $O(V+E)$
    - adjacency matrix: $O(V^2)$
- $O(V + E) \neq O(V^2)$
    - let algo A run in $O(V+E)$
    - let algo B run in $O(V^2)$
    - for dense graph where $E \approx V^2$, algo A and algo B both run in $O(V^2)$
    - for a sparse graph where $E \leq V$, algo A runs in $O(V)$ while algo B runs in $O(V^2)$ still
    - therefore, these two runtime notations are not the same since one is dependent on edges and the other is not
