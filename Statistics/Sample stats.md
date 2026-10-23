Assume $X_1,\ldots,X_n$ are independent and identically distributed (iid), with $E[X_i]=\mu$, $\operatorname{Var}(X_i)=\sigma^2<\infty$, and $n\geq 2$.

## Sample mean

$$\bar X=\frac1n\sum_{i=1}^n X_i$$

$$E[\bar X]=\frac1n\sum_{i=1}^n E[X_i]=\mu$$

Thus, $\bar X$ is an unbiased estimator of $\mu$.

## Variance of the sample mean

By independence,

$$\operatorname{Var}(\bar X)=\frac1{n^2}\sum_{i=1}^n\operatorname{Var}(X_i)=\frac{n\sigma^2}{n^2}=\boxed{\frac{\sigma^2}{n}}$$

## Sample variance

The population variance is

$$\sigma^2=E[(X_i-\mu)^2]$$

First, divide the sum of squared deviations from $\bar X$ by $n$:

$$V_n=\frac1n\sum_{i=1}^n(X_i-\bar X)^2$$

Using $X_i-\bar X=(X_i-\mu)-(\bar X-\mu)$ and $\sum_{i=1}^n(X_i-\mu)=n(\bar X-\mu)$, expansion gives

$$V_n=\frac1n\sum_{i=1}^n(X_i-\mu)^2-(\bar X-\mu)^2$$

Since $E[\bar X]=\mu$, we have $E[(\bar X-\mu)^2]=\operatorname{Var}(\bar X)$. Taking expectations,

$$E[V_n]=\frac1n\sum_{i=1}^n E[(X_i-\mu)^2]-E[(\bar X-\mu)^2]=\sigma^2-\frac{\sigma^2}{n}=\boxed{\frac{n-1}{n}\sigma^2}$$

Thus, $V_n$ underestimates $\sigma^2$ on average. Multiplying by $\frac{n}{n-1}$ corrects the bias:

$$S^2=\frac{n}{n-1}V_n=\frac1{n-1}\sum_{i=1}^n(X_i-\bar X)^2,\qquad \boxed{E[S^2]=\sigma^2}$$

Dividing by $n-1$ gives an unbiased estimator of the population variance.
