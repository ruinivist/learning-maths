# Stirling Numbers

## 2nd kind

ways to divide **n unique** objects to **k non-empty identical** boxes
defined as $S(n,k)$

### using inclusion exclusion

The biggest challenge here is the "non-empty" condition. Assume for a moment we don't have that
restriction then each item can go to any of the $k$ boxes, and finaly we de-arrange that.
Define this as $T = \frac{1}{k!} k^n$

But this has cases where some boxes that are empty, so we start to subtract them.
Define $A_i = \text{count where box i is empty}$
then we just need to subtract $D = \bigcup A_i$ from $T$

There is a $\frac1{k!}$ factor on each of these so for writing it easily I'll just add it at last and work
as if the boxes are labeled too.

$$
\begin{aligned}
A_1 &= \binom k1 (n-1)^k \\
A_2 &= \binom k2 (n-2)^k \\
\ldots\\
A_i &= \binom ki (n-i)^k
\end{aligned}
$$

Sum via inclusion exclusion will gives you

$$
\sum_i (-1)^{i+1} \binom ki (n-i)^k
$$

Note that $i$ here starts from $1$ and he initial term can too be written as $(n-0)^k$ so you can unify it all
as this

$$
S(n,k) = \frac 1{k!} \sum_i (-1)^{i} \binom ki (n-i)^k
$$

### using recurrence

use these boundary conditions, you don't really need the second one but it helps short circuit an otherwise
long path

$$S(n,1)=1\qquad S(n,n) = 1$$

then you have two cases for putting the $n_{th}$ object in,

1. put it in a NEW group like $\{n\}$ and count the rest $S(n-1,k-1)$
2. extend existing group, there's k of those so pick one $kS(n-1,k)$

$$S(n,k) = S(n-1,k-1) + kS(n-1,k)$$
