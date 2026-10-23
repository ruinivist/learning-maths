# Binomial distribution

If $X\sim\operatorname{Bin}(n,p)$, then $X$ counts successes in $n$ independent trials, each with success probability $p$, where $n$ is a nonnegative integer and $0\leq p\leq 1$.

Let $q=1-p$. Choosing which $k$ trials succeed gives

$$\boxed{P(X=k)=\binom nk p^kq^{n-k}},\qquad k=0,1,\ldots,n$$

Write the count as a sum of indicators:

$$X=\sum_{i=1}^n X_i,\qquad X_i=\mathbf{1}_{\{\text{trial }i\text{ succeeds}\}}$$

The $X_i$ are independent Bernoulli random variables with $P(X_i=1)=p$.

## Mean

By linearity of expectation,

$$E[X]=\sum_{i=1}^n E[X_i]=\sum_{i=1}^n p=\boxed{np}$$

## Variance

Since $X_i$ is an indicator, $X_i^r=X_i$ for every integer $r\geq 1$. Thus $E[X_i^2]=E[X_i]=p$, so

$$\operatorname{Var}(X_i)=E[X_i^2]-E[X_i]^2=p-p^2=pq$$

By independence,

$$\operatorname{Var}(X)=\sum_{i=1}^n\operatorname{Var}(X_i)=\boxed{npq=np(1-p)}$$

### Alternatively, count pairs

$\binom X2$ counts pairs of successful trials. There are $\binom n2$ pairs, each successful with probability $p^2$. By linearity,

$$E\left[\binom X2\right]=E\left[\sum_{i<j}X_iX_j\right]=\binom n2 p^2$$

Using $X^2=2\binom X2+X$,

$$E[X^2]=2E\left[\binom X2\right]+E[X]=n(n-1)p^2+np$$

Hence,

$$\operatorname{Var}(X)=E[X^2]-E[X]^2=n(n-1)p^2+np-n^2p^2=np(1-p)$$
