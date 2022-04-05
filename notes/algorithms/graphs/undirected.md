# Undirected Graph

- **Connected**- run DFS or BFS and see you visit all the nodes (keep a count and compare to size of graph)
    - BFS tree from a node is a connected component

- **Articulation Point**- a node that if removed, will split $G$ into 2+ parts
    - $a$ is an articulation point if every path btw $v$ and $w$ contains $a$ 
- **Biconnected Components**- components with no articulation points

## Articulation Points

- Execute DFS while keeping track of additional info 
    - Overall runtime of $\Theta (V + E)$
- A node $u$ is an articulation point if:
    -  $u$ is the root of the DFS tree and has at least 2 children in the tree (not in the graph!)
        - This means the children cannot reach each other in any other way except through $u$
    -  $u$ is not a root of the DFS tree and $u$ has a child with a subtree that has no backedge to one of $u$'s  ancestors
        - This means all the descendants of $u$ must travel through $u$ to reach any ancestors of $u$ in the DFS tree

## Minimum Spanning Trees

- Can be found for undirected, weighted graphs
    - Both algorithms fail on directed graphs
- A tree $T$ of $G$ such that the  sum of the edge weights is minimized
- Can be optimally found using greedy algorithms due to the structure of the problem
- Both algorithms only include an edge in the MST when it is justified by the Cut Property
- Both can run in $O(E \log V)$ time given the correct data structure
- Cut property is a common technique used in proving correctness of gredey MST algorithms
    - A cut is a partition of the vertices of a graph $G$ into two disjoint sets 
    - The cut property states that for any cut $C$ of the graph, if the weight of an edge $e \in C$ is strictly smaller than the weights of all other edges of $C$, then this edge belongs to all MSTs of the graph
        - lightest edge in a cut-set must be in the MST

### Prim's

- Start with a root node and greedily grow the tree otuward, always adding the node that can be reached cheapest from the current node
- Greedy algorithm
- Can stop at any point and have a valid mst that doesn't reach all the nodes
    - optimal substructure 

- $O(E \log V)$ when implemented using a priority queue ADT 
    - priority queue allows us to pick the cheapest vertex in $O(\log V)$ instead of $O(V)$ using just a basic array/list which results in $O(V^2)$ runtime

### Kruskal's

1. Sort the edges from least to greatest ($O(E \log V)$)
    - this is the bottleneck in terms of speed (faster union-find implementations won't help)
2. Insert the next edge in the sorted edge list into the tree if it does not cause any cycles (othewise discard it)

- stopping at any point will not leave you with a valid msg
- implemented using the union-find structure
    - as each edge $(v,w)$ is considered we need to efficiently find the connected components containing $v$ and $w$.
    - if the components are different, there is no path btw $v$ and $w$ and thus no cycle so the edge can be included
        - if the edge is included, the components of $v$ and $w$ should be merged into a single new component

#### Union-Find Data Structure

- Stores graph components (disjoint sets) in a way that supports rapid searching and updating
- can only be used to maintain graph components as we *add* edges (not remove them)
- `Find(u)` will return the name of the set containing $u$
    - `Find(u) == Find(v)` checks if $u$ and $v$ are in the same set
    - $O(\log V)$
    - compress the path (e.g. set pointer directly to set root) after every find operation to make subsequent finds faster
- `Union(A,B)` merges two sets $A$ and $B$ into a single set
    - $O(1)$
    - keep the name of the larger set as the name of the union
- `MakeUnionFind(G)` for a set $G$ will return a UFDS with all elements in separate sets
    -  $O(V)$
