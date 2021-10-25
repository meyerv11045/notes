# Statistics and Sampling Distributions
DEF: a **statistic** is any quantity that can be calculated from sampled data. It is one special case of random variable

The random variables $X_1, ... X_n$ are said to form a simple random sample of size n if 
1) $X_i$'s are independent
2) Every $X_i$ has the same probability distribution

We often say that $X_i$'s are iid (independent and identically distributed random variables)

If we sample without replacement, we can assume $X_i$;s are iid if sample size << population size

## Examples of Statistics
$\bar{x}$. The sample mean is random variable that is a statistic. (population mean would not be a statistic since there is no variance, there is only 1 true value for the entire population)

Since these statistics are random variables, we should be able to compute their pdfs, pmfs, cdfs, etc. 

Method 1: Deduce from info about $X_i$'s
Method 2: Experiment

Example:
$X_i ~ Exp(\alpha)$ is iid for all i in range 1 to n.

$T_n = \sum_{i = i}^n X_i$
$T_n ~ Gamma(n, \frac{1}{\alpha})$

$E(x_i) = \frac{1}{\alpha}$ so $E(X_i) \approx \sum X_i / n$

When we cannot deduce the distribution of a statistic, we run experiments (usually programatically):

We need the:
1. Statistic we want
2. Distribution of the $X_i$'s
3. Number of samples $n$
4. Number of repetitions

As you increase the number of samples, the resulting normal distribution of the statistic will converge to the true value of the statistic. This is the idea behind the central limit theorem. As $n$ increases, the spread decreases. 

Example:
We want a RV $Y$ s,t. $F(y) = e^y$. We can get this using $X \sim Uniform[0,1]$

Take $X = h^{-1}(y) = e^y$ which implies $x = e^y$ so $ln(x) = Y$.

## Central Limit Theorem
$E(\bar{x}) = \sum E(x_i) / n = n \mu  /n = \mu$ where $
\mu$ is the average of $X_i$.

$$ lim_{n -> \infty}P(\frac{\bar{x} - \mu}{\sigma / \sqrt{n}} \leq Z)$$