# Statistics and Sampling Distributions
A sample mean will have variance since each new sample from the population will result in slightly different observed values. This uncertainty in the observed values means the resulting sample mean will also have uncertainty. This uncertainty means the sample mean can be represented with a distribution.

DEF: a **statistic** is any quantity that can be calculated from sampled data. Prior to obtaining data, there is uncertainty as to what the value of the statistic will be so the statistic is a special case of a random variable.

The probability distribution of a statistic is known as its **sampling distribution** to emphasize how its value varies across all possible samples.

The probability distribution of a statistic depends not only on the population distribution (normal, uniform, etc.) and sample size $n$, but also on the method of sampling.

The random variables $X_1, ... X_n$ are said to form a simple random sample of size n if 
1) $X_i$'s are independent
2) Every $X_i$ has the same probability distribution

The above properties are summarized by saying that $X_i$'s are iid (independent and identically distributed random variables).

If we sample without replacement, we can assume $X_i$'s are iid if the sample size $n$ is much smaller than the population size $N$ (i.e. population size is so big that not replacing the sampled values does not really change the probability too much of what is sampeled next). In practice if $\frac{n}{N} \leq 0.05$ (at most 5% of the population is sampeled), we can proceed as if the $X_i$'s form a random sample.

There are two methods for obtaining information about a statistic's sampling distribution:
1) Calculations based on info about $X_i$'s
2) Simulation experiment

## Deriving the Sampling Distribution

**Example 6.3**: (in book)

$X_i \sim Exp(\lambda)$ is iid for all i in range 1 to n where $X_i$ represents the service time for customer $i$. The total service time could then be represented as $T_n = \sum_{i = i}^n X_i$.

1. Set up the cdf using double integrals and a region of integration
2. Differentiating the cdf to get the pdf of $T_n$ will then yield an equation in the form of a gamma pdf with $\alpha = n$ and $\beta = \frac{1}{\lambda}$.

$$T_n \sim Gamma(n, \frac{1}{\alpha})$$

With the distribution for $T_n$, we can easily find the expected value, variance, etc. for the statistic.

## Simulation Experiment
When we cannot derive the distribution of a statistic, we run experiments programmatically:

We need the:
1. Statistic of interest ($\bar{X}, S,$, etc.)
2. Population Distribution (i.e. distribution of the $X_i$'s)
   - Ex: normal with $\mu = 100$ and $\sigma = 15$
3. Number of samples $n$
4. Number of repetitions $k$

A computer then obtains $k$ different random samples, each of size $n$, from the designated population distribution. For each of the $k$ random samples, the value of the statistic is calculated and added to a histogram. The histogram gives the approximate sampling distribution of the statistic. Kernel density estimators perform a similer function except instead of using bins to approximate the pdf, it outputs a smooth line to approximate the pdf. This helps reduce information loss due to the width of bins.

**The more repetitions $k$, the better the approximation** since as $k \to \infty$ the actual sampling distribution emerges. 

As you increase the number of samples $n$, the resulting normal distribution of the statistic will converge to the true value of the statistic. This is the idea behind the central limit theorem- **As $n$ increases, the spread decreases** since the effect of one outlier is less when there are more data points being sampeled.

## Sample Mean's Distribution

Let $X_1, ..., X_n$ be iid from a distribution with mean $\mu$ and standard deviation $\sigma$. Then,

1. $E(\bar{X}) = \mu_{\bar{X}} = \mu$
2. $V(\bar{X}) = \sigma_{\bar{X}}^2 = \sigma^2/n$

So the standard deviation $\sigma_{\bar{X}} = \sigma/\sqrt{n}$

In addition where the sample total $T_n = X_1 + \dots + X_n$, $E(T_n) = n \mu$ and $V(T_n) = n\sigma^2$.

These results show that the $\bar{X}$ distribution becomes more concentrated about the population mean as the sample size increases while the sample total's distribution spreads out more as sample size increases.

Rough proof for property 1: $E(\bar{x}) = \sum E(x_i) / n = n \mu  /n = \mu$ where $\mu$ is the average of $X_i$.

Lemma: $X_1, ..., X_n$ independent random variables:

$$E(a_1X_1 + ... + a_nX_n) = a_1E(X_1) + ... + a_nE(X_n)$$
$$V(a_1X_1 + ... + a_nX_n) = a_1^2V(X_1) + ... + a_n^2V(X_n)$$

$$M_{a_1X_1 + ... + a_nX_n}(t) = M_{X_1}(a_1t) * ... * M_{X_n}(a_nt) $$

This property is the motivating idea behind moment generating function. Its the change of basis that diaglonizes the linear statistics. This is a probabilistic laplace transform.

$$\begin{aligned} 
M_{a_1x_1 + a_2x_2}(t) &= E(e^{t(a_1x_1 + a_2x_2)}) \\
&= \int \int e^{t(a_1x_1 + a_2x_2)} * f_{X_1,X_2}(X_1,X_2) dX_1 dX_2 \\
&= \int \int e^{ta_1x_1} * f_{X_1}(X_1) e^{ta_2x_2} * f_{X_2}(X_2) dX_1 dX_2  \\
&= E(e^{ta_1x_1}) E(e^{ta_2x_2})
\end{aligned}$$

Summing Distributions:
$$ X_i \sim N(\mu_i, \sigma_i^2)$$

$$L = a_1X_1 + ... a_nX_n$$

$$M_{X_i} = e^{t\mu_i + t^2a_1^2\sigma^2/2} = e^{t(a_1\mu_1 + ... a_n\mu_n) + 0.5 t^2 (a_1^2\sigma_1^2 + ... ++ a_n^2\sigma_n^2)} $$
So 
$$X \sim N(\sum a_i \mu_i, \sum a_i^2\sigma_i^2)$$

## Central Limit Theorem
If $X_i$ indepednent and identically distributed with mean $\mu$ and variance $\sigma^2$, then

$$\lim_{n \to \infty} P(\frac{\bar{X} - \mu}{\sigma / \sqrt{n}} \leq z) = P(Z \leq z) = \Phi(z)$$

and 

$$ \lim_{n \to \infty}P(\frac{T_n - n\mu}{\sqrt{n}\sigma} \leq z) = P( Z \leq z) = \Phi(z)$$

where $Z$ is a standard normal random variable.

NOTE: If $n >> 0$ ($n > 30$ is enough) then you can approximate the distribution of the mean by a normal distribution meaning the above central limit theorem holds.

INTERPRETATION: When $n$ is sufficiently large, $\bar{X}$ has an approximately normal distribution with mean $\mu$ and variance $\sigma^2/n$.

The CLT is useful as a shortcut in computing probabilities involving the sample mean since it allows us to use a standard normal such that we don't have to actually find the sample mean distribution.

### Appling the CLT:

$X \sim Gamma(\alpha, \beta)$. If $\alpha >> 0$ then X is approximately normally distributed. This is true because $X = \sum_{i = 1}^\alpha X_i$ where $X_i \sim Exp(\frac{1}{\beta})$. So $X = T_\alpha$ of $X_i$'s so $X$ is approximately normal according to the central limit theorem.

$Y \sim Bi(n,p)$ where $n >> 0$. Then $Y$ is normally distributed since $Y = \sum_{i = 1}^n Y_i$ where $Y_i$ is 1 if success, 0 if failure. $Y \approx NormaL(np, \sqrt{n}\sqrt{p(1-p)})$

## Law of Large Numbers
Two forms with different interpretations/strengths in their proof of convergence.

The mean square of the variance of the mean approaches 0 as the number of samples increases. This requires afinite variance to demonstrate convergence of the mean.

Chebyshev's inequality is stronger in demonstrating convergance as it does not require a finite variance.

Take an interval around $\mu$ of $[\mu - \epsilon, \mu + \epsilon]$.

## Summary
LLN tells us the average tends to the mean with increased number of observations

CLT tells us the average tends to the mean in the shape of a normal distribution