# Directed Graph

- **Strongly Connected**- path from every node to every other node
- Since not all nodes on a graph may be able to reach each other, a graph may be composed of **strongly connected components (scc)** or strong components
- SCC- a set of vertices such that there is a path from every vertex to every other vertex in the set

## Finding Strongly Connected Components

1. Perform DFS (from random start vertex), when a vertex is finished (colored black) push onto a stack
2. Compute the transpose of the graph (flip direction of edges)
3. Run DFS on $G^T$, with the starting vertex being the top of the stack
    - When you get stuck, pop from the stack to restart DFS with a new start ppint 
4. Each tree in the DFS forest of $G^T$ is a strongly connected component 

- Analysis:
    - 2 DFS: $\Theta(V + E)$
    - Transpose of $G$ is $\Theta(V + E)$
    - *Overall Runtime:* $\Theta (V+ E)$

## Topological Sorts

- Only occur on DAGs- directed, acyclic graphs (directed graphs with no cycles)
    - Can be perfomed on disconnected graphs 
- Useful for task scheduling or building a project with dependencies in the correct order (topological sort is just a valid ordering of tasks or dependencies to complete/build in sequential order)
- Can be more than one topological sort 
- How to find topological ordering?
    - Start with vertex with no incoming edges
        - CLAIM: every DAG has a vertex with no incoming edges
        - PROOF: by way of contradiction, suppose there is a DAG and every vertex has an incoming edge. Choose $uv$ and walk backwards from $v$ to $u$. From $u$ find one of its outgoing edges $wu$ and walk backwards to $w$. Continue indefinitely. After $n$ steps, at least one vertex was visited twice, thus a cycle. A contradiction has been reached since the graph is a DAG
            - If graph is disconnected, choose any connected component and repeat the process above
            - If no connected components, there are no edges and evey vertex has no incoming edges
    - For every directed edge $uv$ from vertex $u$ to vertex $v$, $u$ comes before $v$ in the ordering
- Prove via induction every DAG has a topological ordering:
    - Base case, $n = 2$
    - Assume true for $k$ nodes, that a DAG on $k$ nodes has a topological ordering
    - Prove true for $k+1$ nodes that a DAG $G$ on $k+1$ nodes has a topological ordering
    - Given an arbitrary graph $G$ on $k+1$ nodes that is a DAG, find $v$ in $G$ where $v$ is a node with no incoming edges. Remove $v$ to create $G'$, a graph on $k$ Nodes. $G'$ must be a DAG also because if you have a DAG and remove a node, you cannot create a cycle.
    - $G'$ is a DAG on $k$ nodes so it has a topological ordering by the inductive hypothesis
    - Since we removed from $G$ the node $v$ with no incoming edges, we can place $v$ at the front of the topological sort of $G'$ to  produce a topological sort for $G$
- The inductive proof leads to an algorithm:
    - Find a node with no incoming edges, $v$
    - Remove $v$ and its edges from $G, $ $v$ is head of topological sort
        - deleting $v$ with no edges means only need to delete outoing edges so $v$ isn't on anyone's neighbor list
        - need to decrement the count of incoming edges on each of $v$'s neighbors 
    - Recursively find a node $v$ of $G$ with no incoming edges
    - $O(V^2)$ but can be faster $\Theta(V+E)$ if there is a more efficient way to find vertex with no incoming edges instead of a simple $O(V)$ search (there is and it uses dfs)
- CLAIM: If you run a DFS on a DAG, you will not find any back edges (no cycles)
- Better algorithm using DFS:
    - Execute DFS and as each vertex is finished (all edges explored), add it as the head of the topological sort (build the topological sort from back to front)
    - Nodes that get finished first have no further descendants/dependencies so they can be added to the topological sort in order of completion since that means they either have no more dependencies or their dependencies are already in the sort
    - $\Theta(V + E)$

## Shortest-Path Bellman Ford Algorithm

- Can handle negative edge weights and negative cycles in the graph
    - detects negative cycles since they can lead to indeterminate path of length $- \infty$
- Based on idea that repeatedly relaxing the edge weights will eventually converge to the shortest path

```
Bellman-Ford(G, w, s){
	Initialize()
	for i = 1 to |V| - 1 {
		for each edge (u,v) in E {
			Relax(u, v, w)
		}
	}
	
	# check for negative edge cycles
	for each edge (u,v ) in E {
		if d[v] > d[u] + w(u, v) {
			report negative edge cycle exists
		}
	}
}

Relax(u, v, w) {
	if (d[v] > d[u] + w(u, v)) {
		d[v] = d[u] + w(u, v)
		predecessor[v] = u
	}
}
```

- Runtime is $O(VE)$
    - Much slower than dijkstra's
    - Should only be used when potential for negative edge cycles
