# Joint Probability Distributions
Many problems involves several random variables, thus it is useful to have models for the joint behavior of several random variables, especially the case where the variables are independent of each other.

## Joint PMF for 2 DRVs
A single pmf for a DRV $X$ specifies the amount of mass for each possible value of $X$. The joint pmf of DRVs $X$ and $Y$ describes the amount of mass for each possible pair of values $(x,y)$. 

Let $X$ and $Y$ be two DRVs defined on sample space $S$ of an experiment:

$$p(x,y) = P(X = x \cap Y = y) = \sum_x sum_y p(x,y)$$

The marginal pmfs of X and Y:

$$p_X(x) = \sum_y p(x,y)$$

$$p_Y(y) = \sum_x p(x,y)$$

This makes sense since order to get the probability of a certain value of x, we take its probability as the sum over all possible y values. The marginal pmfs are useful for computing probabilites of events involving only one of the RVs.

## Joint PDF for 2 CRVs
A single pdf for a CRV $X$ specifies the amount of mass per unit length for each possible value of $X$ on an interval/set. A joint pdf of CRVs $X$ and $Y$ specifies the amount of mass per unit area for each possible pair of values $(x,y)$. 

Let $X$ and $Y$ be two CRVs and $A$ a two-dimensional set.

$$P[(X,Y) \in A] = \int_A \int f(x,y)dx dy$$

Then $f(x,y)$ is the joint pdf with properties:
1) $f(x,y) \geq 0$
2) $\int_{-\infty}^\infty \int_{-\infty}^\infty f(x,y) dx dy = 1$

![](/static/crv2-pdf.png)

If $A$ is a two-dimensional rectangle:

$$P(a \leq X \leq b, c \leq Y \leq d) = \int_a^b \int_c^d f(x,y)dy dx$$
 
The marginal pdfs for $X$ and $Y$:
$$f_X(x) = \int_{-\infty}^{\infty} f(x,y) dy $$

$$f_Y(y) = \int_{-\infty}^{\infty} f(x,y) dx $$

## Independence of 2 RV

DEF: Two RVs $X$ and $Y$ are independent if $\forall (x,y)$ 

$p(x,y) = p_X(x)*p_Y(y)$ for DRVs

$f(x,y) = f_X(x)*f_Y(y)$ for CRVs

## Independence of n RV
Def: $x_1 ... x_n$ are independent RV if (for any subset $a_1$ to $a_r$) 

for DRV $P(x_{a_1}, ..., x_{a_r}) = P(x_{a_1}) * ... *P(x_{a_r})$

for CRV $f(x_{a_1}, ..., x_{a_r}) = f(x_{a_1}) * ... *f(x_{a_r})$

---
## Multinomial Distribution
Model: n independent trials with replacement with $r$ possible outcomes each. $P_i$ = prob of getting ith outcome $i = 1, ..., r$.

$X_i$ = # times the ith outcome appears

The jpmf of $X_1 ,... X_r$ has a multinomial distribution. 

$$P(X_1, \cdots , X_r) = \frac{n!}{X_1!X_2! \cdots X_r!}P_1^{X_1}P_2^{X_2} \cdots P_r^{X_r}$$ 

Divide by the number of permutations of each element to remove permutations from the total number of ways the elements can be arranged/

---
## Expected Value for Functions of 2 RV
$X, Y$ are RV and $Z = h(X,Y)$.

Remeber that the expected value can be thought of as a weighted average so the same idea extends to functions of 2 RV:

DRV: 
$$E(Z) = \sum_X \sum_Y h(X,Y)P(X,Y)$$

CRV: 
$$E(Z) = \int_{-\infin}^{\infin}\int_{-\infin}^{\infin} h(x,y) dy dx$$

Note: You can change the order of summation/integration when the series is convergent (i dont really understand why)

Propositions:
1) $E(aX + Y) = aE(X) + E(Y)$
2) If $X,Y$ are independent, then $E(X,Y) = E(X)E(Y)$

A counterexample s can be found such that the reverse of 2) does not hold meaning $E(X,Y) = E(X)E(Y)$ does not imply independence of $X$ and $Y$. 


Proof of 1)
$$
\begin{aligned}
 E(aX+Y) &= \sum_X \sum_Y (aX+Y)P(X,Y) \\
    &= a \sum_X \sum_Y X P(X,Y) + \sum_X \sum_Y YP(X,Y) \\
    &= a \sum_X  X \sum_Y P(X,Y) + \sum_Y Y \sum_X P(X,Y) \\
    &= a \sum_X  X \sum_Y P_X(X) + \sum_Y Y \sum_X P_Y(Y) \\
    &= aE(X) + E(Y)
\end{aligned}
$$


 ## Covariance
 DEF: $X,Y$ are RV. Then $Cov(X,Y) = E((x- \mu_x)(Y-\mu_y)) = E(X,Y) - E(X)E(Y)$

### Interpretations
- Covariance measures how much $X$ and $Y$ are spread since $Cov(X,X) = \sigma^2$
- How much are $X$ and $Y$ related
- How much $X$ and $Y$ fail to be independent 
    - $Cov(X,Y) = 0$ does not imply independence as demonstrated by the counterexample to proposition 2 above.
- How linear is the relation between $X$ and $Y$

### Examples
![Graph of covariances](/static/covariance.jpg)

The leftmost graph reprsents $X$ and $Y$ variables highly related in an inversely proportional way meaning when $X$ increases, $Y$ decreases and when $X$ decresases, $Y$ increases.

The rightmost graph represents $X$ and $Y$ variables highly related in a directly proprtional way.

### Properties
$$Cov(aX,Z) = aCov(X,Z)$$

This implies $Cov(aX,aX) = a^2Cov(X,X)$.

$$Cov(aX + bY, Z) =  aCov(X,Z) + bCov(Y,Z)$$

## Correlation
DEF: $X$ and $Y$ are random vars.  
$$Corr(X,Y) = \delta_{x,y} = \frac{Cov(X,Y)}{\sigma_x \sigma_y}$$

Properties:
1) $a,c > 0$ or $a, c <0 $ implies $Corr(aX+b, cY+d) = Corr(X,Y)$
2) $-1 \leq Corr(X,Y) \leq 1$
3) $Corr(X,Y) = \pm 1$ iff $Y = aX +b$ for some $a \neq 0$

Correlation is unrelated to the value of the slope.
Simply means when it is one, the slope is positive/increasing. WHen it is negative one, the slope is negative/decreasing. Correlation of 0 means no relation between the points (points are distributed roughly as a circle/sphere). As the correlation approaches -1 or 1, the circle of points flattens, with the spread increasing.

Independent random variables will have a correlation of 0.
However, uncorrelated random variables do not imply independence.

Correlation does not imply causation!

From a dataset we can compute correlation with the following formula:

$$\delta_{x,y}  = \frac{\sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y})}{(n-1)s_x s_y}$$


## Transformations of RVs
$X$ is a CRV and $Y = h(X)$.

Goal: Find the pdf of $Y$ from the pdf of $X$.

Assume $h$ has an inverse.
$$F_Y(y) = P(Y \leq y) = P(h(X) \leq y) = P(X \leq h^{-1}(y) = F_X(h^{-1}(y)$$ 

Therefore, $f_Y(y) = f_X(h^{-1}(y)) \frac{dh^{-1}}{dy}(y)$

If h has a decreasing inverse, $f_Y(y) = -f_X(h^{-1}(y)) \frac{dh^{-1}}{dy}(y)$

$P(h(X) \leq y) = P(X \leq h^{-1}(y)$ only holds if $h^{-1}$ is increasing. If $h^{-1}$ is decreasing then $P(h(X) \leq y) = P(X \geq h^{-1}(y)$

$$f_Y(h(x)) = f_X(x) \lvert \frac{1}{h'(x)} \rvert$$

## Change of Variables Formula for 2 RVs
$X$ and $Y$ are CRV. 
$U, V = h(X, Y)$

$$f_{(u,v)}(h(x,y)) = f_{x,y}(x,y)\lvert \frac{1}{\frac{\partial u,v}{\partial x,y}} \rvert$$

In the equation above, the denominator is the determinant of the jacobian. This represents the change in areas from X,Y to U,V (remember 3Blue1Brown determinant visualization intuition of differencec between areas).