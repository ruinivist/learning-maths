# Newsvendor problem

This is one of the classic problems from operations research but of course everything as always boils down to probability, statistics and linear algebra.

## The problem

A store must choose a replenishment capacity $RV$ before demand is known, where $RV=s$ is the stocking level.

Demand $X$ is random, with PMF $p(i)=P(X=i)$.

- Each unit sold earns profit $b$.
- Each unsold unit causes a loss $\ell$.
- If demand is greater than $s$, the store can only sell $s$ units.

Find the value of $RV$ (equivalently, $s$) that maximizes expected profit.

## Solution

Let $s$ be the number of units stocked, and let $X$ be the random number of units sold ( demanded ).

Define the profit function:

$$P(s,X)=\begin{cases}bX-(s-X)\ell, & X\le s,\\ sb, & X>s.\end{cases}$$

Here:

- $b$ = profit per unit sold,
- $\ell$ = loss per unsold unit,
- $p(i)=P(X=i)$.

For a given initial number of units stocked, calculate expected profit over the random demand $X$:

$$E[P(X)]_s=\sum_{i=0}^{s}\left[bi-(s-i)\ell\right]p(i)+\sum_{i=s+1}^{\infty}sb\,p(i).$$

Since

$$\sum_{i=s+1}^{\infty}p(i)=1-\sum_{i=0}^{s}p(i),$$

we can write

$$E[P(X)]_s=\sum_{i=0}^{s}\left[bi-(s-i)\ell\right]p(i)+sb\left(1-\sum_{i=0}^{s}p(i)\right).$$

Expanding,

$$E[P(X)]_s=sb+\sum_{i=0}^{s}\left[bi-(s-i)\ell-sb\right]p(i).$$

Now simplify the expression inside the brackets:

$$bi-(s-i)\ell-sb=bi-s\ell+i\ell-sb.$$

Therefore,

$$bi-s\ell+i\ell-sb=(b+\ell)i-s(b+\ell).$$

Factor out $(b+\ell)$:

$$bi-(s-i)\ell-sb=(b+\ell)(i-s).$$

Hence,

$$\boxed{E[P(X)]_s=sb+(b+\ell)\sum_{i=0}^{s}(i-s)p(i)}$$

### The nature of this expected profit at limits

Note that the $i-s$ inside will ALWAYS be negative for the entire sum as $i<s$ so you don't want $s$
to be too large. But my limiting $s$ you also reduce the $sb$ term, so there HAS to be some maxima.

We then anaylse the $E[P]_{s+1} - E[P]_s$ aka the "increase in profit if I stock one more unit"

A lot many terms cancel out and you are left with
$$b - (b+l) \sum_{i=0}^{s}p(i)$$

We would want to keep on stocking as long as this sum is $>0$ so this gets us to
$$\sum_{i=0}^{s}p(i) = P(X \leq S) < \frac b{b+l}$$

Note that the RHS is fixed, so you would want you $s$ such that it is the maximum under that limit.

### Relation to terms as used in other literature

A bit of jargon bloat here that you can ignore, these guys "define imaginary terms" for just math and
equate them and try to reason about it, it's fine if that's what their goal is and they can draw
parallels but let's now try to "name" thing arbitrarily here.

In finanance/op theory/supply chains, they call this the "critical ratio" where $b$ is the underage cost
aka cost of buying one unit too few and $l$ is the cost of buying one unit too many.

$$
\underbrace{bP(X>s)}_{\text{expected marginal benefit}}
\quad \text{vs.} \quad
\underbrace{\ell P(X\le s)}_{\text{expected marginal cost}}
$$

At the cutoff, they balance:

$$
bP(X>s)=\ell P(X\le s)
$$
