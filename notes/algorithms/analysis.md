# Algorithm Analysis

Asymptotic notation captures the growth of a function as its arugments approach infinity. That is, we are concerned with how the algorithms runtime grows as the size of its input $n$ grows. Lets us drop low-order terms and constants to focus on the order of growth as $n$ grows.

## Big O- Worst Case

- Gives an upper bound on an algorithm's runtimes
- $f$ is of order at most $g $ 
- $f(x)$ is $O(g(x))$ iff there exists a $B > 0$ and $b \geq 0$ such that $|f(x)| \leq B|g(x)|$ for all real numbers $x > b$

## Big Omega- Best Case

- Gives a lower bound on an algorithm's runtime
- $f$ is of order at least $g$
- $f(x)$ is $\Omega(g(x))$ iff there exists an $A > 0$ and $a  \geq 0$ such that $|f(x)| \geq A|g(x)|$  for all real numbers $x > a$

## Big Theta

- Not the average case
  - To find the average case, we need to know details about the inputs given to the function and their frequency/probabilities
- Not gauranteed to exist (i.e. algorithm's best and worst case are not the same order e.g. $O(n^3)$ and $\Omega(n)$)
- Tightest gaurantee on runtime of algorithm so use whenever possible
- $f$ is of order $g$ 
- $f(x)$ is $\Theta(g(x))$ iff there exists $A, B > 0$ and $k \geq 0$ such that $A|g(x)| \leq f(x) \leq B|g(x)|$ for all real numbers $x > k$

## Useful Theorems

- Polynomial Orders: let $ f(x) = a_nx^n + a_{n-1}x^{n-1} + .... a_0$ where $a_n \neq 0$
  - $f(x) \in O(x^s)$ where $s \geq n$
  - $ f(x) \in \Omega(x^r)$ where $r \leq n$ 
- $\forall b > 1$ and $\forall x > 0$, we have $log_bn \in O(n^x)$
- $\forall r > 1$ and $\forall d > 0$, we have $n^d \in O(r^n)$

