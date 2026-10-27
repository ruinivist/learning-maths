# Gambler's ruin

## Problem

A gambler starts with $i$ dollars and plays until their fortune reaches $0$ or $N$, where $0\leq i\leq N$. Each independent game wins $1$ dollar with probability $p$ or loses $1$ dollar with probability $q=1-p$, where $0<p<1$.

What is the probability of reaching $N$ before going broke?

## Hitting probability

Let $h_i$ be the probability of reaching $N$ before $0$ starting from $i$. At the endpoints, $h_0=0$ because we are already broke, and $h_N=1$ because we have already reached the target.

For $1\leq i\leq N-1$, the first game moves us to $i+1$ with probability $p$, or to $i-1$ with probability $q$. From there, the chance of reaching the target is $h_{i+1}$ or $h_{i-1}$, respectively. Conditioning on this first step gives

$$h_i=ph_{i+1}+qh_{i-1},\qquad h_0=0,\quad h_N=1$$

### Turn the recurrence into successive differences

Since $p+q=1$, write the left side as $ph_i+qh_i$ and rearrange:

$$ph_i+qh_i=ph_{i+1}+qh_{i-1}\quad\Longrightarrow\quad p(h_{i+1}-h_i)=q(h_i-h_{i-1})$$

Define $d_i=h_i-h_{i-1}$, the increase in our chance of success from having one extra dollar. Then

$$d_{i+1}=\frac qp d_i.$$

Writing $r=q/p$, the differences form a geometric sequence:

$$d_1,\quad d_2=rd_1,\quad d_3=r^2d_1,\quad\ldots,\quad d_i=r^{i-1}d_1.$$

Add the first $i$ differences. The intermediate terms cancel, and $h_0=0$, so

$$h_i=(h_1-h_0)+(h_2-h_1)+\cdots+(h_i-h_{i-1})=d_1\sum_{k=0}^{i-1}r^k.$$

The remaining unknown is $d_1$. Use the other endpoint, $h_N=1$:

$$1=d_1\sum_{k=0}^{N-1}r^k\quad\Longrightarrow\quad d_1=\frac{1}{\sum_{k=0}^{N-1}r^k}.$$

Substituting back gives, for $1\leq i\leq N$,

$$h_i=\frac{\sum_{k=0}^{i-1}r^k}{\sum_{k=0}^{N-1}r^k}.$$

### Fair game: equal increases

If $p=q=1/2$, then $r=1$. Every difference equals $d_1$, so the numerator has $i$ copies of $1$ and the denominator has $N$:

$$h_i=\frac{i}{N}.$$

For example, with a target of $10$ dollars, starting at $3$ gives a success probability of $3/10$. Each extra dollar adds $1/10$ to that probability.

### Biased game: sum the geometric sequence

If $p\ne q$, then $r\ne1$, and the finite geometric-sum formula gives

$$\sum_{k=0}^{i-1}r^k=\frac{1-r^i}{1-r}.$$

The common factor $1-r$ cancels between the numerator and denominator:

$$h_i=\frac{(1-r^i)/(1-r)}{(1-r^N)/(1-r)}=\frac{1-r^i}{1-r^N}.$$

Combining the two cases, including the endpoints,

$$h_i=\begin{cases}\displaystyle\frac{i}{N},&p=q=\frac12,\\[6pt]\displaystyle\frac{1-(q/p)^i}{1-(q/p)^N},&p\ne q.\end{cases}$$

The fair case needs its own formula because substituting $r=1$ into the biased formula gives $0/0$.

The chance of ruin is $1-h_i$. These are the only two eventual outcomes: from any interior fortune, $N$ consecutive losses would force ruin, and this sequence has positive probability $q^N$. By independence, the probability of avoiding both boundaries for $kN$ games is at most $(1-q^N)^k$, which tends to zero.

## Remembering the formula

The odds against winning a single game are $q/p$: probability of losing divided by probability of winning. For $p\ne q$,

$$\boxed{P(\text{reach }N\text{ before }0\mid\text{start at }i)=\frac{1-(\text{odds against})^i}{1-(\text{odds against})^N}}$$

Use the starting fortune $i$ in the numerator and the target fortune $N$ in the denominator. At $i=0$ the numerator is zero; at $i=N$ it matches the denominator.

For a fair game, the odds against are $1$, so use $i/N$ instead.

## Connection to a random walk

A fair random walk starting at $1$ reaches $b$ before $0$ with probability $1/b$. This is the gambler's ruin problem with $i=1$ and $N=b$; see the random walk problem in [Properties of expectation](../Practice/Properties%20of%20expectation.md).
