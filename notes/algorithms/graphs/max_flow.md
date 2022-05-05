# Network Flow

- A general class of problems that share a common structure
- Bipartite Matching problem is one type of network flow problem that has many applications (e.g. matching jobs to available machines)

## Ford-Fulkerson Method

- Continue finding augmenting paths and augmenting the flow until no more augmenting paths from $s$ to $v$ exist
- Max Flow = sum of bottlenecks in each augmenting path
- Time complexity depends on algorithm used to find augmenting paths
    - Can use DFS but this gives a runtime dependent on the max flow in the graph $f$, $O(fE)$
    - Can use BFS to get runtime independent of max flow in graph: $O(E^2 V)$
    - In practice, the average runtimes are better than the worst cases
- [Video](https://www.youtube.com/watch?v=LdOnanfc5TM&t=0s)

### Edmonds Karp Algorithm

- Method for finding augmenting paths using BFS 
- Uses BFS to find the shortest (in terms of # edges) augmenting path from $s$ to $t$ at each iteration 
    - Beneficial compared to DFS arbitrarly long augmenting path since the longer the path, the higher chance of getting a small bottleneck value which will result in more iterations to get the max flow 
- Rule: Only explore an edge if its remaining capacity > 0
    - remaining capacity = capacity - flow 
- Repeat until termination criteria:
    1. Run BFS from $s$ to $t$ to get the shortest path (whichever reaches $T$ first)
        - Can take residual edges as long as they satisfy the exploration rule
    2. Find bottleneck value by taking min of remaining capaciites of the edges on the path 
    3. Augment (update) the flow of the forward edges (+ bottleneck value) and the residual edges (- bottleneck value)
- Termination Criteria: all outgoing edges from $s$ have remaining capacity = 0 (i.e. no more augmenting paths from $s$ to $t$)
- [Video](https://www.youtube.com/watch?v=RppuJYwlcI8)