# Greedy Algorithms

- When they work in solving a problem optimally it implies something about the strucutre of the problem itself
    - i.e. There is a local decision rule that one can use to construct optimal solutions
- Finding cases where greedy algorithms work well and proving their performance is challenging
- Any algorithm that follows the problem-solving heurisitc of making the locally optimal choice at each stage with the intent of finding a global optimum
- Follow a form of:
    - select a candidate greedily according to some heuristic
    - if adding the candidate does not corrupt feasability of the solution, add it to your current solution
    - repeat until finished 
- Two methods for proving a greedy algo produces optimal solution to a problem
    - Greedy Algorithm Stays Ahead
    - Exchange Argument
- Applications:
    - Shortest paths in a graph
    - Interval Scheduling
    - Minimum Spanning trees in an undirected graph
    - Minimum cost aboresence problem in directed graph
    - Huffman code construction in data compression
    

- When to use the greedy approach?
    - Does the *problem* display *optimal substructure*? 
    - Does your *algorithm* have the *greedy choice property*?
    - If both questions above can be answered yes, then the greedy approach is good, but might also be able to use dynamic programming
        - DP useful in the case of overlapping subproblems 


## Optimal Substructure

- Property of problems that can be solved with a greedy algorithm or dynamic programming
- Describes a problem if an optimal solution can be constructed from optimal solutions of its subproblems
- Has optimal substructure: shortest path, fractional knapsack
- Does not have optimal substructure: 0/1 knapsack, longest path on non-DAG

### Structure of a Proof

- Assume $O$ is an optimal answer
- Remove an element $x$ from $O$ (often last element) to create $O'$
- Redefine the constraints of the problem for which $O'$ is a solution 
- Prove that $O'$ is an optimal answer for this redefined problem
    - Often a proof by contradiction: assume $O$ is optimal but $O'$ is not
    -  Find $O^*$,the optimal answer to the redefined problem
    - Add $x$ to $O^*$ to make a *new* answer to the original problem
    - Contradiction reached in that $x + O^*$ is better than $O$ which was optimal
    - Therefore, $O'$ must be optimal and so the problem has optimal substructure

### Ex: Shortest Path

- Assume the shortest path from $u$ to $v$ is $P$ and $w \in P$.
- Remove the end of the path from $w$ to $v$ to create $P'$ which is a path from $u$ to $w$. 
- Is $P'$ the shortest path from $u$ to $w$? 
- By way of contradiction assume $P$ is optimal but $P'$ is not. Let $P^*$ be the optimal path from $u$ to $w$. If we add the previously removed edge from $w$ to $v$ to $P^*$ then we have created a new path from $u$ to $v$ which is more optimal than $P$. This is a contradiction, so therefore $P'$ must be optimal and so the shortest path problem has optimal substructure. 

## Shortest Paths in a Graph

- Given a strongly connected directed graph $G = (V, E)$ and a start node $s$
    - Each edge $e$ has a length $\ell_e \geq 0$
- Goal: determine shortest path from $s$ to every other node in the graph
- Greedy algorithms take advantage of the optimal substructure of the shortest  path
    - longest path does not have same optimal substructure (unless working with a DAG) so cannot use a greedy algorithm

### Dijkstra's Algorithm

```
let S be set of explored nodes
	for each u in S we store a distance d(u)

Initially S = {s} and d(s) = 0

while S != V
	select an unexplored node with at least one edge from S
	
	
visited = {s}
undiscovered = {V - s}
for i = 1 to |V| 
	dist[i] = infinity // O(V)
```

- Cannot handle negative edge weights 
- BFS is faster for shortet path of unweigghted graph (could give all edges equal weight and run dijkstra's')

## Interval Scheduling

- We have $n$ requests each $i$th request corresponding to an interval of time starting at $s(i)$ and finishing at $f(i)$
- A subset of the requests is *compatible* if no two of them overlap in time
- Goal: Determine largest compatible subset as possible 
- Greedy rule/heuristic for choosing request:
    - choose request a finishes first

```
let R be set of all intervals
Sort R by finish time
let G be empty solution set

for interval in R:
	if G is empty: 
		add first interval to G
	else:
		if interval does not overlap with last interval in G:
			add interval to G
```

- This algorithm runs in $O(n \log n)$ 
    - Sort is $O(n \log n)$
    - Iterate through intervals is $O(n)$

### Proof of Correctness

- We will use the stay ahead argument 
- We will prove for each $r \geq 1$, the $r$th interval in the algorithm's solution $G$ finishes no later than the $r$th interval in the optimal schedule
- Note that $|G| = k$ and $|O| = m$ and we want to show $|G| = |O|$ in order to prove the greedy algorithm creates an optimal solution

#### Proof:

We will prove via induction: for all $r \leq k$ we have $f(i_r) \leq f(j_r)$.

Base Case (r = 1): The algorithm selects the request $i_1$ with the minimum finish time so it is clearly an optimal first choice $f(i_1) \leq f(j_1)$.

For $r>1$ we will assume the inductive hypothesis is true ($f(i_{r-1}) \leq f(j_{r-1})$) for $r - 1$ and will try to prove it for $r$. Since $O$ consists of nonoverlapping intervals, $f(j_{r-1}) \leq s(j_r)$. Therefore, combining this with the inductive hypothesis implies $f(i_{r-1}) \leq s(j_r)$. This means interval $j_r$ is in the set of available intervals at the time when the greedy algorithm selects $i_r$. The greedy algorithm selects the available interval with the smallest finish time, therefore $f(i_r) \leq f(j_r)$. This completes the induction steps so we have proven the optimality of the greedy algorthim's set $A$.

So far we have only proven that the greedy algorithm's solution is as good as the optimal solution. To finish we need to prove $|G| = |O|$.

#### Proof: 

By way of contradiction, assume $G$ is not optimal so $|O| > |G|$. This means there is a requests in $O$ that starts after $f(j_k)$ and therefore after $f(i_k)$. This means there was a compatible interval left to choose from that the greedy algorithm did not choose and opted to stop instead. This is a contradiction from how the greedy algorithm was designed so therefoer $|G| = |O|$.

## Fractional Knapsack

- Thief robbing a store finds $n$ types of metallic dust 
- The $i$th dust is worth $v$ per ounce with $w_i$ total ounces available
- Knapsack can hold total of $W$ Ounces.
- What is the max value of dust that can fit in the knapsack?
- Solution: Calc value/oz and then add as much of the most valuable as possible then move to the next valuable, and repeat until the sack is full
    - this approach is greedy and takes advatnage of the optimal substructure of the problem

### Prove Optimal Substructure

Suppose $O$ is the optimal packing of the knapsack of size $W$ and value $val(O)$ give a list $L$ of possible values. Remove one item $i$ from the knapsack with weight $w_i$ and value $v_i$ to get a new packing $O'$ of a knapsack of size $W - w_i$ and choosing from the set of items $L - i$. By way of contradiction, assume $O'$ is not optimal. This means we have a higher value packing. If we add the discarded stuff $w_i$ to this higher value packing, then we have a solution to the overall packing that is worth more than $O$. A contradiction has been reached, therefore the problem has optimal substructure.

[Optimal Substructure](https://www.cs.ucr.edu/~yihans/teaching/141/f20/141F20/discussion/worksheet4.pdf)

### Prove Greedy Choice Property

Suppose $O$ is an optimal solution and does not include the first choice $C_1$ made by the greedy algorithm. Let $w$ be the weight of the most valuable item. Remove $w$ oz of any other item and replace that with $w$ oz of the most valuable algorithm. We have now increased the value of $O$ which is a contradiction. Therefore, this $w$ oz of the most valuable item was already in the packing of the optimal solution $O$. Our first greedy choice could be a part of any optimal solution.

## Proving Correctness of Greedy Algorithms

- Showing the problem has optimal substructure and the algorithm has the greedy choice property **does not** prove the algorithms correctness
- Can prove correctness of the algorithm by:
    - Induction 
    - Contradiction (suppose your algorithm makes a mistake)

- useful techniques:
    - stay ahead argument
    - exchange argument 
        - given greedy answer and optimal answer, bring the greedy over into the optimal at the place where they first differ, where the results should be a contradiction
- Example: Greedy Camping problem can be proven correct using *stay ahead argument* and *induction*

### Exchange Argument

- Incrementally modify the greedy algorithm's solution into the optimal solution
- Steps:
    1. Label your algorithm's solution $G$ and a general optimal solution $O$
    2. Compare $G$ with $O$ 
        - by contradiction assume $G \neq O$ 
        - typically you isolate a simple example of a difference
            - element of $O$ not in $G$ and element of $G$ not in $O$ or
            - 2 consecutive elements in $O$ in a different order than they are in $G$
    3. Exchange
        - Swap the elements in question in $O$ (either swap element out and another in for first case or swap order of elements in second case)
        - Argue $O$ is no worse than before
        - Argue if you continue swapping, you can eliminate all the differences between $G$ and $O$ in a polynomial number of steps without worsening the quality of the solution
        - Thus $G$ is optimal 

- The goal in exchange argument is to show how to modify $O$ to create a new solution $O'$ with the following properties:

    1. $O'$ is at least as good of solution as $O$ (or equivalently $O'$ is also optimal), and

    2. $O'$ is “more like” $G$ than $O$.

- The creative part that differs for each algo/problem is determining how to modify $O$ to create $O'$

    - Good place to start is think about how $G$ is constructed and look to make the modification at the first point where the algorithm makes a choice for $G$ that is different than what is in $O$

- Notes:

    - remember to argue why the elements you are swapping even exist out of order or not in one solution but in the other

- [Cornell Notes](https://www.cs.cornell.edu/courses/cs482/2007su/exchange.pdf)

### Stay Ahead Argument

- Inductively prove that under some measure, the partial solutions produced by the greedy algorithm "stay ahead" of the partial solutions produced by an optimal algorithm
- [Cornell Notes](https://www.cs.cornell.edu/courses/cs482/2003su/handouts/greedy_ahead.pdf)

## Data Compression

- A prefix code means no code for a single letter is the prefex of another letter
    - this makes decoding significantly easier
- encodings can be visualized as binary trees
    - prefix codes have all letters as leaves of the tree
    - to get an optimal encoding for a document, we want the most frequently occuring characters to be closest to the top of the tree (less bits to represent them)
    - shortest tree representation is the most optimal 
- Full binary tree- tree where each non-leaf node has two children

### Shannon-Faro Algorithm

- Build tree with top down approach
- Need one leaf for every symbol in the alphabet
- Divide symbols into 2 sets where total frequency of each set is near equal
- A set of size 2 is finished, Represent each symbol w/ 1 bit
- Recursively divide sets of size > 2 into two balanced sets 
- Turns out the resulting encoding is not optimal (counterexamples exist)
    - Pretty good results still so it was used in practice for a while since no better alternatives existed 

### Huffman Coding Algorithm

- Lossless compression algorithm that is better than shannon-faro
- Goal: Reduce total number of bits used to encode a piece of text without losing any information (optimal coding scheme)
- Code Trees- describe how to encode a letter
    - traversing a left edge has a value of 0
    - traversing a right edge has value of 1 
    - therefore, we want the most frequently occuring characters to be closest to the root of the code tree since this means it will have the smallest code
    - optimal code tree will be a full binary tree 
- Recursively builds up the tree from the lowest frequency characters at the deepest part of the tree to the most frequently occuring characters closest to the root of the tree 
- Greedy algorithm since it can be stopped at any point and the codes built for the included symbols at that point are optimal

``` 
huffman(S):
	if |S| = 2:
		return a tree with root and 2 leaves from S
		
	else:
		S = S \ {u, v} where u, v are two chars w/ lowest frequency
		S = S + new char w w/ frequency f_w = f_u + f_v 
		T' = Huffman(S)
		T = T' w/ leaf w removed and replaced with interior node + 2 children u, v
		return T 
    
```

- Runtime is $\Theta(n \log n)$ when using a priority queue that can find the least frequently occuring character in $O(\log n)$
    - $T(n)  = T(n-1) + 2* \text{find min}$
        - The best method for finding a min is a priority queue which is $O(\log n)$
        - $T(n) = T(n - 1) + 2(\log n)$
        - Recurrence relation can be solved via unrolling to find $T(n) \in \Theta(n \log n)$
- Proof of optimal substructure: in an optimal encoding tree the sibling pair at the lowest level of the tree will have the smallest frequency
- [Video Explanation](https://www.youtube.com/watch?v=dM6us854Jk0)