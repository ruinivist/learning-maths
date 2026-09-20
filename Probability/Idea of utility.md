# Utility

"Utility" tries to generalise and define "value" of a set of consequences.
So far many games or situations involving probability and expected returns
use monetary value mapped to consequences and assume that the "participant"
is perfectly rational; this is not always the case and we try to model that
here.

For example, even under the expected monetary value case, if given the choices
between guaranteed \$50 vs 50-50 chance on getting nothing vs \$100, people
would behave differently. Even more so if scale those values even more.
The difference then becomes obvious.

## Defining utility

Define an "action" as something that, for a common consequence set, changes
the probabilities associated with the individual consequences.

For $Cs = \{C_1, C_2, \dots, C_n\}$, let

$C = \text{my best outcome from all } Cs$

and

$c = \text{my worst outcome from all } Cs$.

Utility $u$ assigns each consequence a numerical value according to how
desirable it is to me.

We normalise the scale by defining

$u(c) = 0$

and

$u(C) = 1$.

For any other consequence $C_i$, we determine its utility by comparing:

1. receiving $C_i$ for certain, versus
2. a lottery which gives $C$ with probability $p$ and $c$ with probability
   $1-p$.

We vary $p$ until I am indifferent between these two choices. At that point,
we define

$u(C_i) = p$.

For example, if receiving $C_i$ for certain feels equivalent to a lottery
with a $70\%$ chance of receiving $C$ and a $30\%$ chance of receiving $c$,
then

$u(C_i) = 0.7$.

Thus, utility gives us a numerical representation of how much I value each
possible consequence.

## Expected utility

Suppose Action 1 gives consequence $C_i$ with probability $p_i$, while
Action 2 gives consequence $C_i$ with probability $q_i$.

Then their expected utilities are

$$
EU(A_1) = \sum_{i=1}^{n} p_i u(C_i)
$$

and

$$
EU(A_2) = \sum_{i=1}^{n} q_i u(C_i).
$$

We choose the action with the greater expected utility.

So there are really two separate things:

- $p_i$ or $q_i$ describes how likely each consequence is under an action.
- $u(C_i)$ describes how valuable that consequence is to me.

Expected monetary value is a special case of this. If utility is linear with
money, then maximizing expected utility gives the same decision as maximizing
expected monetary value.

However, utility does not have to be linear.

For example, consider a guaranteed $\$50$ versus a $50$-$50$ gamble between
$\$0$ and $\$100$. Both have expected monetary value $\$50$:

$$
E[\text{gamble}] = 0.5(\$0) + 0.5(\$100) = \$50.
$$

But I may still prefer the guaranteed $\$50$. In utility terms, this means

$$
u(\$50) > 0.5u(\$0) + 0.5u(\$100).
$$

Utility therefore lets us account for how a person values outcomes and risk,
rather than assuming that monetary value itself is always the correct measure
of desirability.
