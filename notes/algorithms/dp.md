# Dynamic Programming

- A methodical way to try all possible answers (An exhaustive search)
    - Focus is on ordering computations in a way that avoids duplicate work  to get a polynomial time answer
- Can be used to solve problems that have optimal substrucutre and overlapping subproblems but lack the greedy choice property so greedy algorithm will not work
    - overlapping subproblems- many problems are calculated repeatedly

- Good for optimization problems (shortest, maximal, minimum, etc.)

## Top-Down

- Implemented using recursion
- Starts from the end and works backwards
- Memoization- store results of subproblems to be reused since DP problems often have overlapping subproblems
    - Runtime = subproblems * time per subproblem

## Bottom-Up

- Avoids recursion to save the memory cost of the call stack
    - Call stack is vulnerable to a stack overflow error
    - Exactly same computation as recursive/memoized version
- Starts from the beginning 
- Can often be cleaner and more efficient than top-down
- Downside is you have to determinethe ordering of your calculation of subproblems such that previous subproblem results can be used to compute future subproblem results 
    - Essentially a topological sort of subproblem dependency DAG to reveal the order to compute the subproblems
- Saves storage space 
- Clearer runtime than the recursive version



## Fibonnaci Numbers

- $F_1 = F_2 = 1$
- $F_n = F_{n-1} + F_{n-2}$

### Naive Algorithm

```
fib(n):
	if n <= 2: return 1
	else: return fib(n-1) + fib(n-2)
```

- Exponential runtime: $\Theta(2^n)$

### Memoized DP Algorithm

- Memoized for efficiency

```
memo = {}
fib(n):
	if n in memo: return memo[n]
	if n <= 2: return 1
	else: 
		f = fib(n-1) + fib(n-2)
		memo[n] = f
		return f 
```

- Overall runtime is $\Theta(n)$
    - Memoizied calls of the subproblems cost $\Theta(1)$
    - $n$ non-memoized calls (`fib(1)`, `fib(2)`, ... `fib(n)`)
    - nonrecursive work per call is $\Theta(1)$

### Bottom-Up DP Algorithm 

```
fib = {}
for k in range(1, n+1):
	if k <= 2: 
  	f = 1
	else: 
		f = fib[k-1] + fib[k-2]
  fib[k] = f
return fib[n]
```

- Iteratively builds up to the solution instead of recursively working backwards
    - Oftentimes more efficient due to less function calls
- Choosing the order to compute the subproblems was easy in this case (just increasing integers up to $n$)
    - However, this can be the tricky part for other problems since you want subsequent calls to utilize already computed subproblems to avoid repeat work

## Shortest Path

- $\delta(s,v) = \min\{w(u,v) + \delta(s,u) | (u,v) \in E\}$ with base case $\delta(s,s) = 0$
- Exponential runtime for naive implementation
- Can memoize to get better runtime
- Takes infinite time if there are cycles 
    - subproblem dependencies should be acyclic
- For DAG, runtime is $O(V +E)$
    - time for subproblem $\delta(s,v) = indegree(v)$
    - total time = $\sum_{v \in V} indeg(v) = O(E + V)$ 
- Bellman Ford algorithm comes from extending this idea to limit $k$ edges in the path form $s$ to $v$: $\delta(s,v)_k$
    - results in increased subproblems but can deal with cycles
    - Runtime $O(VE)$

## 0/1 Knapsack

- Does not have the greedy choice property so cannot use greedy solution
- Has overlapping subproblems so dp approach should work

### DP Algorithm

Let $N$ be the set of objects where $n$ indicates an object. Let $C$ be the capacity of the knapsack and let $s_n$ indicate the size of object $n$. Let $v_n$ indicate the value of object $n$.

- If item $n$ does fit in the knapsack (i.e. $s_n \leq C$ ) choose the maximum result of the two subproblems:
    1. Do not include object $n$: $value(N \setminus \{n \}, C)$ 
    2. Include object $n$: $v_n + value(N \setminus \{n\}, C - s_n)$

- If item $n$ doesn't fit in the knapsack (i.e. $s_n > C$) just find  $value(N \setminus \{n\}, C)$

### Runtime

- Pseudo-polynomial since they are computable but depend on the capacity and size picked  
- $O(2^n)$


## Maximum Sum of List Subset

- Given a list $L$ of $n$ numbers, select a subset $S$ of $L$ such that their sum is maximized and no two numbers in $S$ are adjacent in $L$

```
maxsum(<x1, ... ,xn>) = max{x_1 + maxsum(<x3, ... xn>), maxsum(<x2, ..., xn>)}
```

Memoized version:

``` 
cache = {}
function max_sum(<x1, x2, ..., xn>) {
	if length(<list>) = 1: return x1
	
	
	if hash(<x3, x4, ..., xn>) in cache:
		with_x1 = cache[hash(<x3, x4, ..., xn>)]
	else: 
		with_x1 = max_sum(<x3, ..., xn>)
		cache[hash(<x3, x4, ..., xn>)] = with_x1
	
	if hash(<x2, x3, ..., xn>) in cache:
		without_x1 = cache[hash(<x2, x3, ..., xn>)]
	else: 
		without_x1 = max_sum(<x2, x3, ..., xn>)
		cache[hash(<x2, x3, ..., xn>)] = without_x1
		
	return max(x1 + with_x1,without_x1)	
}
```



## NP-Complete

- While certain problems are NP-complete, for certain input sizes, the solution can be calculated using dynamic programming in a reasonable time



## Resources

- [MIT 6.006 DP I](https://www.youtube.com/watch?v=OQ5jsbhAv_M)