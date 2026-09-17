# Coupon collector

## Problem

( I like my formulation better )

There are $n$ distinct cards that are available, each bag of chips can have any with equal probability.

Define random variables

- $T =$ count of bags I open to get all cards
- $D_m$ = count of distinct cards in the first $m$ bags

Solve for

- $E[T]$
- $P[T = k]$
- $E[D_m]$
- $P[D_m = k]$

**bonus**
analyse the limiting cases as well

---

## Solving for $E[T]$

There's two solution one from FSA and other a bit of "magic" ( that I kind of dislike as such "guess" like
solutions are hard to reason and can deceptively be wrong for many other cases )

### using FSA

think of the two states, the first step where I am $E_i$ and where a transition can take me $(E_i,E_{i+1})$
where $E_i = \text{waiting time for getting to n cards}$

naturally, $E_n = 0$. Now note that at $E_i$, I already have $i$, so new ones are $n-i$

$$
\begin{aligned}
E_i &= 1 + \frac{i}{n} E_i + \frac{n-i}{n} E_{i+1}\\
E_i - E_{i+1} &= \frac{n}{n-i}
\end{aligned}
$$

This'll make telescopic sums

$$
\begin{aligned}
E_0 - E_1 &= \frac{n}{n-0}\\
E_1 - E_2 &= \frac{n}{n-1}\\
\ldots\\
E_{n-1} - E_n &= \frac{n}{n-(n-1)}\\
\end{aligned}
$$

which if you factor out $n$ gives you a harmonic sum of first $n$ natural numbers.

$$
E_0 = n(\frac1n + \frac1{n-1} + \ldots + \frac11) = nH_n
$$

### or you can do a waiting time argument of probabilities to next

Let $P(i) = \text{probab of getting a new card if I have i cards}$, then note how probabs change

$$
\begin{aligned}
P_0 &= \frac nn\\
P_1 &= \frac{n-1}n\\
P_2 &= \frac{n-2}n\\
\ldots\\
P_{n-1} &= \frac1n\\
P_n &= 0
\end{aligned}
$$

Note that here $p$ is probab of success and I want $T = \text{number of trials till first success}$ so we have
$T \sim \text{geometric}$ and hence we can to $E[T] = \frac1p$

If you inverse those probabs and sum those over you get the same result.

> I'm not very confident somehow with this approach, even though I know how it works

---

## Solving for $P[T=k]$

Going about it directly is tricky, what we do is solve for $P(T>k)$ which means probab that after $k$
trials I still haven't got all cards, and then use that result to solve for $P[T=k] = P[T>k-1] - P[T>k]$.

Now under assumption that $k$ trials are done,
Define $A_i = P(\text{card i is still missing after those k trials}) = (\frac{n-1}{n})^k$
Similarly $A_i \cap A_j = P(\text{2 cards are missing now}) = (\frac{n-2}n)^k$

This'll be then based on the count of missing cards $m$ as $(\frac{n-m}n)^k$.

treat $i$ as the cardinality as well because of the combined set in question, at the end we'll have $i = n$ too.
Note that terms would be repeated solely based on cardinatly, a pair will have the same proba, so we can count
pairs.

$$
P(T>k)
=
P\left(\bigcup_i A_i\right)
=
\sum_i (-1)^{i+1}\binom{n}{i}
\left(\frac{n-i}{n}\right)^k
$$

---

## Solving for $E[D_m]$

Expected count of distinct cards I have after $m$ trials

This uses the idea of **decomposing sum to components and then applying linearity**

Define

$$
I_i =
\begin{cases}
1, & \text{if card type } i \text{ has appeared in the first } m \text{ draws}\\
0, & \text{otherwise}
\end{cases}
$$

$D_m = \sum I_i$, such a decomp allows you to cleanly apply linearity as

$$E[\sum I_i] = \sum E[I_i]$$

Note that here since each card is same as any other, by symmetry we have all $E_i$ to be same but
even if not handling of different probabs would be easier.

Now the nice thing about expectation of an indicator is it's just the probab ( trivial to see )
$$E[I_i] = P[I_i] = 1 - \text{never appeared in m draws} = 1 - (\frac{n-1}n)^m$$

Same for all so the result us just $n [1 - (\frac{n-1}n)^m]$

---

## Solving for $P[D_m = k]$

This is tricky because unlike expecation you cannot invoke linearity to decompose the sum.

The way to go is to choose which $k$ appear in $\binom nk$ ways and then map them to $m$ trials (boxes).
Obviously we need $m>=k$. Note that we need to map such that boxes are non-empty ( else we don't have $m$ trials ).
The trials you can treat to be ordered, this'll give you $m! S(m, k)$ ways.
The toal ways in denom are $n^m$ ( for each trial you have m choices, again ordered )

$$P[D_m = k] = \frac{\binom nk k!S(m,k)}{n^m}$$
