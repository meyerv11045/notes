# Divide and Conquer

- Class of algorithms in which one breaks the input into several smaller parts, solves the problem in each part recursively, and then combines the solutions to these subproblems into an overall solution
- Analyzing runtime of these algorithms requires solving a recurrence relation
    - *Recurrence Relation*- bounds running time recursively in terms of running time on smaller instances
- Used to reduce the running time of a brute force polynomial algorithm to a lower polynomial (instead of exponential to polynomial)



## Recurrence Relations

- We will use mergesort for an example:
- $T(n) \leq 2 T(n/2) + cn$ where base case $T(2) < c$
- Solving the above recurrence relation involves getting $T$ to the LHS of the inequality
- Can unroll the recursion to identify a pattern amongst the levels that can be summed until the base case (subproblem of constant size)
    - At level $j$ of the recursion, the number of subproblems has doubled $j$ times so there are now a total of $2^j$ subproblems on that level
    - However, each subproblem's size has been cut in half $j$ times so each problem has a size $n/2^j
    - Since the work to split a problem and combine its results is linear, the work done for each suproblem is at most $cn/2^j$
    - Therefore, level $j$ contributes $2^j (cn/2^j) = cn$ work to the total runtime
    - We want to sum over all levels. How many levels are there?
        - Since we are dividing the input in half each time until it reaches a size of 2, the number of levels to reduce an input of size $n$ to $2$ by halving each time is $\log_2 n$ 
        - Summing $cn$ work over $\log n$ Levels gives total runtime of $O(n \log n)$
    - This runtime holds for any algorithm satisfying the recurrence relation above by halving the input each time and spending only linear time for the division and recombining of subproblems