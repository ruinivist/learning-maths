# Gambler's ruin

## Problem

A gambler starts with $i$ dollars and plays until their fortune reaches $0$ or $N$, where $0\leq i\leq N$. Each independent game wins $1$ dollar with probability $p$ or loses $1$ dollar with probability $q=1-p$, where $0<p<1$.

What is the probability of reaching $N$ before going broke?

## Hitting probability

Let $h_i$ be the probability of reaching $N$ before $0$ starting from $i$. Conditioning on the first game gives

$$h_i=ph_{i+1}+qh_{i-1},\qquad h_0=0,\quad h_N=1$$

Rearranging in terms of successive differences,

$$h_{i+1}-h_i=\frac qp(h_i-h_{i-1})$$

So the differences form a geometric sequence. Summing them and using the boundary conditions gives

$$h_i=\begin{cases}\displaystyle\frac{i}{N},&p=q=\frac12,\\[6pt]\displaystyle\frac{1-(q/p)^i}{1-(q/p)^N},&p\ne q.\end{cases}$$

For a fair game, the chance of reaching the target is the fraction of the way there: $h_i=i/N$. The chance of ruin is $1-h_i$.

## Connection to a random walk

A fair random walk starting at $1$ reaches $b$ before $0$ with probability $1/b$. This is the gambler's ruin problem with $i=1$ and $N=b$; see the random walk problem in [Properties of expectation](../Practice/Properties%20of%20expectation.md).
