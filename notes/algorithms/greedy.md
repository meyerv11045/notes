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

## Dijkstra's 

- cannot handle negative edge weights 

``` 
visited =. {s}
undiscovered. = {V - s}
for i = 1 to |V| 
	dist[i] = infinity // O(V)
```

- BFS is faster for shortet path of unweigghted graph (could give all edges equal weight and run dijkstra's')



## Longest Path

- is not a greedy problem since it doesnt have optimal substructure for undirected graphs
- DAGs do have optimal substructure and allow a longest path to be built up greedily



## Fractional Knapsack

- Thief robbing a store finds $n$ types of metallic dust 
- THe $i$th dust is worth $v$ per ounce with $w_i$ total ounces available
- Knapsack can hold total of $W$ Ounces.
- What is the max value of dust that can fit in the knapsack?
- Solution: Calc value/oz and then add as much of the most valuable as possible then move to the next valuable, and repeat until the sack is full
    - this approach is greedy and takes advatnage of the optimal substructure of the problem



## Optimal Substructure

- Optimal solution to a problem relies on the optimal solution to smaller subproblems
- Has optimal substructure: shortest path, fractional knapsack
- Does not have optimal substructure: 0/1 knapsack, longest path on non-DAG



## When to use Greedy Approach

- Does the *problem* display optimal substructure? 
- Does your *algorithm* have the greedy choice problem?
    - can the first choice be part of some optimal solution?
- If both questions above can be answered yes, then the greedy approach is good, but might also be able to use dynamic programming



## Proving Correctness of Greedy Algorithms

- By induction
- By contradiction
    - suppose your algorithm makes a mistakee
- useful techniques:
    - stay ahead argument
    - exchange argument 