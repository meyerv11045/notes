# Greedy Algorithms

- When they work in solving a problem optimally it implies something about the strucutre of the problem itself
    - i.e. There is a local decision rule that one can use to construct optimal solutions
- Finding cases where greedy algorithms work well and proving their performance is challenging
- Any algorithm that follows the problem-solving heurisitc of making the locally optimal choice at each stage with the intent of finding a global optimum 
- Cut property is a common technique used for proving greedy algorithms
    - A cut is a partition of the vertices of a graph $G$ into two disjoint sets 
    - The cut property states that for any cut $C$ of the graph, if the weight of an edge $e \in C$ is strictly smaller than the weights of all other edges of $C$, then this edge belongs to all MSTs of the graph
        - lightest edge in a cut-set must be in the MST

- Two methods for proving a greedy algo produces optimal solution to a problem
    - Greedy Algorithm Stays Ahead- 
    - Exchange Argument- 

## Applications

- Shortest paths in a graph
    - exploits the structure of shortest path
- Minimum Spanning trees in an undirected graph
- Minimum cost aboresence problem in directed graph
- Huffman code construction in data compression