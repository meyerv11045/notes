# Ch. 3 Solving Problems by Searching

- Search: how can an agent look ahead to find a sequence of actions that will eventually achieve its goal
- Search Algorithms
    - Informed- agent can estimate distance from goal
    - Uninformed- no estimate available
- This chapter assumes knowldege of the environment (ch. 4 deals with unknown env)
- Goals organize behavior by liiting the objectives and potential actions
- Fully observable, deterministic, known envs have a solution to any problem as a fixed sequence of actions
    - Can ignore percepts (Open-loop system in control theory)
    - with potentially incorrect models or nondeterministic envs, better to use closed-loop approach the monitors the perceps and adjusts accordingly
- My life as a search problem in a partially observable, nondeterministic, unknown env:
    - I create a plan to achieve my goals but adjust to experience as I execute on the plan and make sure I have contingency plans for outcomes outside of my control
- Search problem:
    - State space- set of possible states the env can be in
        - can be represented as graph w/ vertices as state and directed edges as actions
        - can be infinite as in the case of recursively defined objects (see Donald Knuth's example)
    - Initial state the agent starts in
    - Goal state (can be multiple or a property that applies to infinite states)
    - Actions- set of actions that can be executed for given state
    - Transition model-describes action -> state mapping
        - $T: S \times A \to S$ where
            - $S$ is state space
            - $A$ is action space
            - $s_0 \in S$ is initial state
            - $G \sub S$ is goal state(s)
    - Action Cost Function- gives cost of applying action $a$ to state $s$ to reach state $s'$
        - reflects the performance measure
- path- sequence of actions
- Solution- path from initial state to goal state
    - optimal- lowest path cost among all solutions
- abstraction- removing detail from a representation to produce the minimally relevant model for a problem
    - critical for allowing useful intelligent agents (too much detail could overwhelm)

### Ex: 8-puzzle

- State Space has $9!/2 = 181,400$  unique states
- branching factor $b = 3$ b/c while 4 directions to move, we will never redo the action to get to the current state (only case it would be 4 is on the first state with the middle being empty, but every subsequent action will be 3)

## Search Algos

- Search Tree- nodes correspond to states and edges correspond to actions
- best-first search- choose a node $n$ from frontier (unexplored) with a min value of some evaluation function $f(n)$. if it is the goal state,  return it, otherwise expand it to generate the children nodes
    - diff eval functions give diff specific algorithms
- Deciding which node from the frontier of the search tree to expand next is based on the evaluation function which the key difference between many search algos
- Datastructures:
    - node has state, parent, action, and path cost fields
    - queue of some kind is used to store the frontier
        - priority- pops node w min cost for an eval fn
        - fifo- bfs
        - lifo (stack)- dfs
    - can store reached states in a hash-table/lookup table
- *algorithms that cannot remember the past are doomed to repeat it*
    - important for not traversing redundant paths which can result in computational explosion
- graph search- checks for redudant paths
- tree-like search- does not check for redudant paths to save memory since the structure of the problem does not pose the issue of redudant paths

## Measuring Performance

- Completeness- is algorithm gauranteed to find a solution given one exists and report a failure when one does not exist
    - algo must be systematic in how it explores infinite search spaces so that it can eventually reach any state connected to the initial state
    - can be complete without having an ubberbound on time to find
- Cost optimality
- Time complexity
- Space complexity

## Uninformed Search

- No info on how close a state is to the goal
- exponential complexity search problems cannot be solved with uninformed techniques for anything but the smallest instances
- *Iterative deepening is the preferred uninformed search method when the search state space is larger than can fit in memory and the depth of the solution is not known.*

### Breadth-First Search

- Cost optimal when all actions have $=$ cost
- Systematic and thus complete on infinite search spaces
- Best-first search with node's depth as evaluation function
- $O(b^d)$ time and space requirements where $b$ is the branching factor and $d$ is the depth in the search tree
    - branching factor $b$ means that expanding a node generates $b$ additional nodes
- memory requirements are bigger issue than execution time (which are still an issue in themselves)

### Dijkstra's Algorithm / Uniform-Cost Search

- Cost optimal when actions have $\neq$ cost
- while breadth-first search spreads out in waves of uniform depth—first depth 1, then depth 2, and so on—uniform-cost search spreads out in waves of uniform path-cost
- Best-first search with Path-Cost as evaluation function
- $O(b^{1 + C^*// \epsilon})$ is time and space complexity
    - $C^*$ is the cost of the optimal solution
    - $\epsilon > 0$ is a lower bound on the cost of each action
    - Can be much greater than $O(b^d)$ due to exploring large trees of actions with low costs before exploring paths with a high-cost and more useful action
    - When all costs are equal, $O(b^{d+1})$ so its similar to BFS
- Considers all paths systematically in order of increasing cost, never getting caught going down a single infinite path (assuming that all action costs are $> \epsilon > 0$) so its complete
- relaxation- update the cost to get to vertex $v$ from vertex $u$  if the cost would be lowered by the edge weight $w$
    - cost starts artificially high at infinity and is updated as shorter paths are found

- greedy strategy but structure of the problem allows cost optimal paths

### Depth-First Search

- expands deepest node in frontier first
    - Best-first search with negative depth as eval function
- Not cost-optimal (returns first path it finds) and incomplete (can get stuck going down an infinite path)
- better for problems where tree-like search is feasible so DFS doesn't keep track of reached nodes and thus has smaller memory requirements $O(bm)$ where $m$ is max depth of tree
- backtracking search (a variant) uses even less memory

### Depth-limited and Iterative Deepening Search

- version of DFS where we supply a depth limit $\ell$ and treat all nodes at $\ell$ as if they have no successors
- $O(b^{\ell})$ time complexity and $O(b\ell)$ space complexity
- depth limit requires knowledge of the problem, and is oftentimes not best determined till after solving the problem
- iterative deepening search solves the problem of picking a good value for $\ell$ by trying all values: first 0, then 1, then 2, and so on—until either a solution is found, or the depth- limited search returns the *failure* value rather than the *cutoff* value.
    - best of DFS and BFS (low memory but $O(b^m)$ runtime and complete on acyclic state spaces with optimal cost)

### Bidirectional Search

- Simultaneously expand the frontiers from the start state and the goal state and hope they meet
- idea is that $b^{d/2} + b^{d/2} << b^d$ (50k times less when $b=d=10$)
- complete and optimal cost

## Informed (Heuristic) Search

- Uses domain-specific hints about the location of goals to find solutions more efficiently than uninformed strategy
    - uses heuristic function $h(n)$
    - Ex: for route finding on a map, a good heuristic is the straight line distance from current node to the goal node
        - note how the heuristic is good b/c of our knowledge of how the problem is structured (maps)

### Greedy Best-First Search

- First expands node with lowest $h(n)$ (node that appears to be closest to goal)
    - Best-first search with $f(n) = h(n)$
- Incomplete in infinite search spaces
- $O(|V|)$ but a good heuristic can reduce it to $O(bm)$ on certain problems

### $A^*$ Search

- Best-first search with eval fn of $f(n) = g(n) + h(n)$
    - $g(n)$ = path cost from initial state to node $n$
    - $h(n) =$ estimated cost of best/shortest path from $n$ to goal node
- complete assuming non-zero action costs and solution exists or state space is finite 
- admissible heuristic- never overestimates the cost cost to reach a goal (optimistic)
    - if admissible then $A*$ is cost optimal
- consistent heuristic if for every node $n$ and its successor $n'$ generated byan action $a$, we have $h(n) \leq c(n, a, n') + h(n')$
    - triangle inequality
    - Ex: straight line distance
    - every constent heuristic is admissible but not vice versa
- efficient b/c it prunes away search tree nodes not needed for finding an optimal solution
- Weighted $A^*$ trades off some optimality for searching smaller amount of state space so the solution can be found quicker
- Memory usage is a main issue
    - Beam search is a variant that limits the size of the fronteir by keeping only the $k$ nodes with the best $f$-scores (thus fewer nodes are expanded) or by keeping only nodes within $\delta$ of the best $f$-score
    - Iterative-deepening $A^*$ search gives the benfits of $A^*$ w/o the requirement to keep all reached states in memory at the cost of revisiting some states (important and commonly used algorithm)

## Heuristic Functions

- The cost of an optimal solution to a relaxed problem (fewer restrictions) is an admissible heuristic for the original problem and is therefore consistent
- Can use ml to learn good heuristics from expereince (previously solved problems)

