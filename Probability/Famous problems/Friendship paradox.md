# Friendship paradox

> On average, your friends have more friends than you do.

It's a paradox because the wording seems contradictory but if you elborate
you can see why it holds.

Define $D_1 = \text{pick a random friend you have and count their friends}$,
Now define $D = \text{number of friends you have}$.
If you do it for a population, $E[D_1] > E[D]$.
This is because at "one-hop" the sampling is biased to move to people that
have a LOT of friends hence pulling up $D$, the distribution has changed.
This is the intuitive idea.

## Mathematically

Using the same defn for $D = \text{number of friends}$

In the graph $G$ with edge set $E$, if I then choose a random edge $e$,
the distribution gets reweighted as more edges to someone make them more
likely to be selected.

Define total number of edges to be $C_e$, from $E[D]$, and you have modeled
"friendship" as bidirectional edge but for a moment assume the graph is
directed, we still have bidirectional friendshipt but instead just have 2
edges for it, this makes reasoning easier in maths.

Now you get $C_e = n E[D]$ where $n$ is the number of nodes.

$$
P(any\ edge) = \frac 1{n E[D]}
$$

Now ask, what is the probab $P(D_1 = d) = P(\text{picking someone with d friends at 1 hop})$
this will simply be $d \times P(any\ edge)$. Also, $\frac 1n = p = \text{probab of randomly choosing someone}$

$$P(D_1 = d) = \frac {dp}{E[D]}$$

then the expectation is
$$E[D_1] = \sum_d d \frac {dp}{E[D]} = \frac {E[D^2]}{E[D]}$$

use $var = E[D^2] - E[D]^2$.

$$E[D_1] = E[D] + \frac {Var(D)}{E[D]}$$

## What about the next hop $D_2$?

I find this one to be the "more acute" paradox in this whole scenario as you would except that a similar
re-weighing of distribution would happen on the next hop.

From 0 hops to first hop, wee change the "distribution" that was getting sampled, from a weighing on
equal for every node to a distribution based on in-degrees defining the likelihood.

If I'm already at a distribution that's sampled based on degrees, a second hop does not change that.
From 0 to 1 hop, my node became $d$ time more likely if I had $d$ edges to me, now if I pick one of mine
and go out from there, that's $\frac 1d$ and it cancels out the $d$ factor, there's' no change in distribution
at all.

so $E[D_2] = E[D_1]$
