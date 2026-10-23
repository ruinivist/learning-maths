## Indicator variables

The idea is very useful to count "expected number of [something]", since contribution of each of that "something" is either 1 or 0.

$$I_i=\begin{cases} 1 & \text{if event }i\text{ occurs} \\ 0 & \text{otherwise} \end{cases}$$

Expectation too naturally decomposes to sum of probabilites ( in fact you can derive the slicing theorem this way )

As a trivial example, if 10 people each flip a coin, what's the expected number of heads?

Define $I_i=1$ if person $i$ gets heads, otherwise 0.

$$E[X]=\sum_{i=1}^{10}P(I_i=1) =10\left(\frac12\right)=5$$

The count itself is $X=\sum_{i=1}^{10}I_i$: each head contributes $1$. Taking expectations turns this count into a sum of probabilities.

## Moments

Suppose we want the averages of higher powers, $X^2,X^3,\ldots$, which give large values of $X$ more weight. The $r$th ordinary moment is $E[X^r]$.

Let $X$ count heads in four independent fair coin tosses. We can find its moments by counting successful groups first.

### Count groups with indicators

Let $A_i$ be the event that toss $i$ is heads, and $I_i$ its indicator. Then

$$X=\sum_{i=1}^{4}I_i,\qquad E[X]=\sum_{i=1}^{4}P(A_i)=2$$

With $X$ heads, $\binom{X}{2}$ counts pairs of heads and $\binom{X}{3}$ counts triples. Products of indicators count exactly these groups:

$$\binom{X}{2}=\sum_{i<j}I_iI_j,\qquad \binom{X}{3}=\sum_{i<j<k}I_iI_jI_k$$

Taking expectations and using linearity,

$$E\left[\binom{X}{2}\right]=\sum_{i<j}E[I_iI_j]=\sum_{i<j}P(A_i\cap A_j)=\binom42\left(\frac12\right)^2=\frac32$$

$$E\left[\binom{X}{3}\right]=\sum_{i<j<k}E[I_iI_jI_k]=\sum_{i<j<k}P(A_i\cap A_j\cap A_k)=\binom43\left(\frac12\right)^3=\frac12$$

These are binomial moments: expected numbers of successful groups. Linearity does not require independent groups; independence of the tosses gives the probabilities $1/4$ and $1/8$.

### Recover powers by linearity

Start with pairs, expand the product, then apply linearity:

$$E\left[\binom{X}{2}\right]=E\left[\frac{X(X-1)}{2}\right]=\frac{E[X^2]-E[X]}{2}$$

Rearrange to recover the second moment:

$$E[X^2]=2E\left[\binom{X}{2}\right]+E[X]=2\left(\frac32\right)+2=5$$

Repeat with triples:

$$E\left[\binom{X}{3}\right]=E\left[\frac{X(X-1)(X-2)}{6}\right]=\frac{E[X^3]-3E[X^2]+2E[X]}{6}$$

$$E[X^3]=6E\left[\binom{X}{3}\right]+3E[X^2]-2E[X]=6\left(\frac12\right)+3(5)-2(2)=14$$

Each step uses moments already found. In general,

$$E\left[\binom{X}{r}\right]=\frac{1}{r!}E[X(X-1)\cdots(X-r+1)]$$

The product has leading term $X^r$ and lower powers of $X$, so we can solve for $E[X^r]$ using lower moments.

The first two moments also give $\operatorname{Var}(X)=E[X^2]-E[X]^2=5-4=1$.

### What distribution work did we skip?

The distribution route first requires $P(X=x)=\binom4x/16$:

| $x$      | $0$    | $1$    | $2$    | $3$    | $4$    |
| -------- | ------ | ------ | ------ | ------ | ------ |
| $P(X=x)$ | $1/16$ | $4/16$ | $6/16$ | $4/16$ | $1/16$ |

Then, for example,

$$E[X^2]=\sum_{x=0}^{4}x^2P(X=x)=\frac{0+4+24+36+16}{16}=5$$

Counting groups needed only the probabilities that specified tosses were all heads. We skipped finding the probability of each possible total head count.

### Summary

Count successful groups to find $E[\binom{X}{r}]$. Expand $X(X-1)\cdots(X-r+1)$, apply linearity, and solve for $E[X^r]$ using lower moments.

## Slicing theorem

I always found it a bit unintuitive, so I'll try to do it once and for all.

For a nonnegative integer-valued RV, basically a count, think of $X=I_1+I_2+\cdots$, where the indicators are defined on $X$ itself:

$$I_k=\mathbf{1}_{\{X\geq k\}}$$

So $I_1$ adds $1$ if $X\geq 1$, $I_2$ adds $1$ if $X\geq 2$, and so on.

Naturally, if $X=4$, the first four indicators contribute $1$ each and all later ones contribute $0$.

We don't know beforehand where the $1$s stop, but since the later terms add nothing, let's just sum to infinity:

$$X=\sum_{k=1}^{\infty}\mathbf{1}_{\{X\geq k\}}$$

Take expectations:

$$E[X]=\sum_{k=1}^{\infty}E[\mathbf{1}_{\{X\geq k\}}]$$

For indicator variables, the expectation is just the probability of the event. This gives the discrete case:

$$\boxed{E[X]=\sum_{k=1}^{\infty}P(X\geq k)}$$

For nonnegative continuous $X$, the corresponding formula replaces the sum with an integral:

$$\boxed{E[X]=\int_0^{\infty}P(X>t)\,dt}$$

## Higher moments of an indicator

If $X_i$ is an indicator with $P(X_i=1)=p$, then $X_i\in\{0,1\}$. For every integer $n\geq 1$,

$$X_i^n=X_i,\qquad \boxed{E[X_i^n]=E[X_i]=p}$$

All positive integer moments are the same. In particular,

$$\operatorname{Var}(X_i)=E[X_i^2]-E[X_i]^2=p-p^2=p(1-p)$$

This above is the variance for a Bernoulli distribution.
