# Conditioning on next relevant outcome

I feel like I would've definitely reached for GP summation if I did not have a notion that
this is effectively the same just "mentally" you can skip the steps and NOT see the GP at all.

## Problem

Given a fair, dice find probability of getting a 1 before a 6.

## Solution as a GP sum

This is trivial, the game ends when you get a 1 or a 6, define $A_i = \text{ending in i moves}$
Then you have,
end at $A_1$ as (1),
$A_2$ as (not 1 or 6)(1)
$A_3$ as (not 1 or 6 twice)(1)

Define $a = P(1) = a$
That $P(\text{not 1 or 6 is}) = 2/3 = r$, the GP then is sum over all $A_i$

$$P(\text{end with 1}) = a + ar + ar^2 + \ldots = a / (1-r) = 1/2$$

## Solution as "ignoring non-meaningful states"

The meaningful states are just getting a 1 or a 6, this is what the game ends on.

$$P(1 = \text{ended with 1} | \text{1 or 6} = \text{game ended}) = 1/2$$
which comes out pretty naturally

I was pleasantly surprised on this though I saw it as a "trick", it helps to understand that you
can pretty much derive GP via this probabilistic argument.

## Derivation via probability

Define $a = P(1), b = P(6), r = P(rest = ignored)$, events being $A = 1\ end$, $B = 6\ end$

$$P(\text{end with 1}) = a + ar + ar^2 + \ldots $$
But
$$P(\text{end with 1} | \text{1 or 6}) = P(A | A\ or\ B) = a / a + b$$

Since $a+b+r = 1$, we have $a+b = 1-r$, so if you equate the two sides and cancel out $a$

$$1 + r + r^2 + \ldots = 1/1-r$$

There exercise does more to "convince" than to extract any sort of mathematical insight here.
