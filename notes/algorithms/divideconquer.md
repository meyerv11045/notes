# Divide and Conquer

- Class of algorithms in which one breaks the input into several smaller parts, solves the problem in each part recursively, and then combines the solutions to these subproblems into an overall solution
- Analyzing runtime of these algorithms requires solving a recurrence relation
    - *Recurrence Relation*- bounds running time recursively in terms of running time on smaller instances
- Used to reduce the running time of a brute force polynomial algorithm to a lower polynomial (instead of exponential to polynomial)
- General model for divide and conquer algorithm
    - Divide input into two pieces using only constant time
    - Solve the two subproblems on each piece using recursion
    - Combine the results into one solution using only linear time

## Recurrence Relations

- We will use mergesort for an example:
- $T(n) \leq 2 T(n/2) + cn$ where base case $T(2) < c$
- Solving the above recurrence relation involves getting $T$ to the LHS of the inequality
- Can unroll the recursion to identify a pattern amongst the levels that can be summed until the base case (subproblem of constant size)
    - At level $j$ of the recursion, the number of subproblems has doubled $j$ times so there are now a total of $2^j$ subproblems on that level
    - However, each subproblem's size has been cut in half $j$ times so each problem has a size $n/2^j$
    - Since the work to split a problem and combine its results is linear, the work done for each suproblem is at most $cn/2^j$
    - Therefore, level $j$ contributes $2^j (cn/2^j) = cn$ work to the total runtime
    - We want to sum over all levels. How many levels are there?
        - Since we are dividing the input in half each time until it reaches a size of 2, the number of levels to reduce an input of size $n$ to $2$ by halving each time is $\log_2 n$ 
        - Summing $cn$ work over $\log n$ Levels gives total runtime of $O(n \log n)$
    - This runtime holds for any algorithm satisfying the recurrence relation above by halving the input each time and spending only linear time for the division and recombining of subproblems
- General form of recurrence relation for divide and conquer:
    - $T(n) = aT(n/b) + f(n)$
    - $a$- number of recursive calls at a level
    - $b$- how much the input size is shrunk
    - $f$- the work done at a level
- Master Theorem:
    - $\log_b n = h$ is the height of the recursive tree ($b^h = n$)

## MaxMin

- Goal: Find maximum and minimum of a set $S$

```
MaxMin(S):
	if |S| = 2:
		return (max(s[0], s[1]), min(s[0], s[1])) # O(1)
	else
		divide S into S1 and S2 # O(1)
		max1, min1 = MaxMin(S1) # T(n/2)
		max2, min2 = MaxMin(S2) # T(n/2)
		
		return (MAX(max1, max2), MIN(min1, min2)) # 2 comparisons
```

- Recurrence relation:
    - $T(n) = 2T(n/2) + 2$ where $T(2) = 1$
    - $O(n)$ because 
        - $\log_2 n$ levels of recursion
        - Each problem at each level performs $2$ operations of work
        - Therefore each level $i$ performs $2^i$
        - Summing over all the levels to get the total amount of work yields
            - $\sum_{i=1}^{\log_2n} = 2^{\log_2n + 1} - 2 = 2 * 2^{\log_2n } - 2 = 2n - 2$ 
            - [Sum of Power Property](https://math.stackexchange.com/questions/1254605/sum-of-powers-of-2-from-1-to-logn)
        - Therefore $O(n)$ total work
        - Helpful to draw out the recursion tree and the corresponding tree of work done

## kth Smallest Element

- Goal: Find $k$th smallest element in an unsorted set of $n$ elements
    - elements only need to support comparison operator

1. Randomly divide $n$ into groups of size 5
2. Find the median in each group using 6 comparisons
3. Recursively find $m^*$, the median among the medians
4. Compare each element in the unknown sections to $m^*$ and place them in the appropriate set $A > m^*$ or $B < m^*$
5. If  
    1. $k = |B| + 1$ then $m^*$ is the $k$th element
    2. $k \leq |B|$ then the $k$th element is in $B$ and can be found recursively 
    3. $k > |B|$ then $k$th element is in $A$ and can be found recursively 

- $T(n) \leq T(\lceil \frac{n}{5} \rceil) + T(\frac{7n}{10}) + O(n)$ can be solved to yield $O(n)$ runtime
    - recursively find median of medians. one median in each group of 5 so therefore $\lceil \frac{n}{5} \rceil$ recursive calls 
    - recursively solve problem on the remaining elements which in the worst case could be a set of size $\frac{7n}{10}$
    - dividing $n$ into groups of $5$, finding the median in all the groups of $5$ and partitioning the unknown values around $m^*$ takes $O(n)$ time