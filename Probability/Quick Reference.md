# Continuous random variables: quick reference

Let $X$ have probability density function (PDF) $f$.

$$
f(x)\ge 0,\qquad \int_{-\infty}^{\infty} f(x)\,dx=1.
$$

Probabilities are areas under the density:

$$
P(a<X<b)=\int_a^b f(x)\,dx.
$$

For a continuous random variable, $P(X=x)=0$, so including or excluding either endpoint does not change this probability.

The cumulative distribution function (CDF) gives the probability up to $x$:

$$
F(x)=P(X\le x)=\int_{-\infty}^{x} f(t)\,dt.
$$

At every point where $f$ is continuous, $F'(x)=f(x)$. More generally, this equality holds almost everywhere.

Expected values, when the integrals exist:

$$
E[X]=\int_{-\infty}^{\infty} x f(x)\,dx,
\qquad
E[g(X)]=\int_{-\infty}^{\infty} g(x)f(x)\,dx.
$$
