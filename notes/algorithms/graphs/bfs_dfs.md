# Basic Graph Algorithms

## Breadth First Search

- Given graph $G = (V,E)$ and source vertex $s$
- Explores edges of G to visit every vertex reachable from $s$
- Computes the distance (smallest # of edges) to from $s$ to each vertex
- Explores all edges at depth $k$ before exploring any edges at depth $k + 1$
- Marks explored vertices as visited so they are not reexplored
- Creates a breadth-first forest comprising several breadth-first trees 
    - each level in a breadth-first tree represents all the nodes at that depth from the source node


### Analysis

- Enqueing and dequeing take $O(1)$ time
- All nodes are added to the queue when exploring the entire graph so this takes $O(V)$ time (overhead for initialization)
- Once a vertex is dequeued, its entire adjacency linked list is scanned (adding vertices to the queue that have not been visited) 
    - Since all the adjacency lists must be scanned in their entirety, it takes $\Theta(E)$ time
    - We explore all edges $\Theta(E))$
        - each edge explored once in undirected graph
        - each edge explored twice in directed graph
- Total runtime is $O(V + E)$ linear to the size of the adjacency list of $G$

## Depth First Search

- Searches deeper in the graph when possible and when it gsets stuck, the search backtracks
- Creates a depth-first forest comprising several depth-first trees 
- time stamps when each vertex is disocvered and when the search finishes examining the vertex's neighbors (adjacency list)
- $\Theta(V + E)$ since all edges are traversed and all edges are visited

### Edge Classification

- Can classify edges in a graph based on how they are discovered when running DFS
- tree edge
- backward edge
    - goes from $v$ to an ancestor of $u$ in the DFT
    - happens when $v$ disocvers $u$ while $u$ has been discovered but not finished yet and $u$ is an ancestor of $v$
- forward edge 
    - goes from $u$ to a descendant of $u$ in the DFT 
    - happens when $v$ discovers $u$ while $u$ is finished and $u$ was discovered after $v$
- cross edge 
    - between $u$ and $v$, neither is ancestor of the other in DFT
    - happens when $v$ discovers $u$ while $u$ is finished and $u$ was discovered before $v$
- edge classification will change depending on where you start building the DFT from 