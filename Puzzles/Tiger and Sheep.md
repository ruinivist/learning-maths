# Tiger and Sheep

There are $n$ tigers and 1 sheep. Only 1 tiger can attempt ( and it will always succeed if it
does so ) to eat a sheep at any time. Eating a sheep makes it a sheep as well.
Will any sheep survive?

## Solution

The point of this problem is to be able to MODEL it and learn how we even do game theoretic modelling like that.

Let $n$ be the number of tigers, and define

$$
E(n)=
\begin{cases}
1 & \text{if the sheep is eaten}\\
0 & \text{otherwise}
\end{cases}
$$

Define each tiger's utility as

$$
U=
\begin{cases}
2 & \text{eats sheep and survives}\\
1 & \text{eats grass and survives}\\
0 & \text{dies}
\end{cases}
$$

If a tiger eats the sheep, it becomes a sheep surrounded by $n-1$ tigers. Hence,

$$
U_{\text{eat}}(n)=2[1-E(n-1)]
$$

$$
U_{\text{grass}}(n)=1
$$

A rational tiger eats iff

$$
U_{\text{eat}}(n)>U_{\text{grass}}(n)
$$

$$
2[1-E(n-1)]>1
\iff E(n-1)=0
$$

Therefore,

$$
\boxed{E(n)=1-E(n-1)}
$$

With the initial condition $E(0)=0$, solving the recurrence gives

$$
\boxed{E(n)=\frac{1-(-1)^n}{2}}
$$

For $n=100$,

$$
E(100)=\frac{1-(-1)^{100}}{2}=\boxed{0}
$$

**Therefore, the sheep survives.**

### A quicker way

is to just look at the recurrence only, the utility argument only clouds things here.

Let $E(n)=1$ if the sheep is eaten by $n$ tigers, and $0$ otherwise.

If a tiger eats the sheep, it becomes a sheep facing $n-1$ tigers. It will therefore eat only if that new sheep would survive.

Hence,

$$
E(0)=0,\qquad E(n)=1-E(n-1)
$$

Solving the recurrence,

$$
\boxed{E(n)=\frac{1-(-1)^n}{2}=n\bmod 2}
$$

Since $100$ is even,

$$
E(100)=\frac{1-(-1)^{100}}{2}=0
$$

Therefore, **the sheep survives**.

## A harder follow-up using game theory

Suppose there are **3 perfectly rational tigers** and **1 sheep** on an island.

Each tiger simultaneously decides whether to attempt to eat the sheep, under the following rules:

- Attempting to eat costs $c$ units of energy, regardless of success.
- If multiple tigers attempt, exactly one is chosen uniformly at random to eat the sheep.
- The successful tiger receives a reward $R$ and turns into a sheep, as in the original problem.
- Tigers that do not attempt receive zero payoff.
- All tigers know the rules and maximize their expected utility.

Assume $c=R/2$.

**Problem:** If each tiger independently attempts to eat with probability $p$, find the symmetric mixed-strategy Nash equilibrium $p^*$ and the probability that the original sheep gets eaten.

### Solution: Mixed-Strategy Nash Equilibrium

**1. Model the strategies**

Let $p$ be the probability that each tiger attempts to eat the sheep. By **symmetry**, all three tigers use the same mixed strategy.

Consider one tiger. The number of other tigers attempting is

$$
X\sim\operatorname{Binomial}(2,p)
$$

Hence,

$$
P(X=0)=(1-p)^2
$$

$$
P(X=1)=2p(1-p)
$$

$$
P(X=2)=p^2
$$

If our tiger attempts while $X=k$ others attempt, its probability of winning is $1/(k+1)$. Since the winner faces two remaining tigers, it survives by the original problem's parity argument.

**2. Calculate expected utility**

The tiger receives reward $R$ if it wins and always pays the cost $c$ for attempting.

Using the **law of total expectation**,

$$
U_A=R\sum_{k=0}^{2}\frac{P(X=k)}{k+1}-c
$$

Expanding,

$$
U_A=R\left[(1-p)^2+\frac{2p(1-p)}{2}+\frac{p^2}{3}\right]-c
$$

Simplifying,

$$
\boxed{U_A=R\left(1-p+\frac{p^2}{3}\right)-c}
$$

Abstaining has zero payoff:

$$
U_N=0
$$

**3. Apply the Nash equilibrium condition**

In a **mixed-strategy Nash equilibrium**, a player must be indifferent between all pure strategies played with positive probability. Otherwise, it would prefer one action over randomizing.

Therefore,

$$
U_A=U_N
$$

Substituting $c=R/2$,

$$
R\left(1-p+\frac{p^2}{3}\right)-\frac R2=0
$$

Dividing by $R$,

$$
1-p+\frac{p^2}{3}=\frac12
$$

Multiplying by $6$,

$$
6-6p+2p^2=3
$$

$$
2p^2-6p+3=0
$$

Applying the quadratic formula,

$$
p=\frac{6\pm\sqrt{36-24}}{4}
$$

$$
p=\frac{3\pm\sqrt3}{2}
$$

Since $0\le p\le1$, we discard the larger root:

$$
\boxed{p^*=\frac{3-\sqrt3}{2}\approx0.634}
$$

**4. Calculate the probability of the sheep being eaten**

The sheep survives only if all three tigers independently choose not to attempt.

Thus,

$$
P(\text{survives})=(1-p^*)^3
$$

By the **complement rule**,

$$
P(\text{eaten})=1-(1-p^*)^3
$$

Substituting,

$$
P(\text{eaten})=1-\left(\frac{\sqrt3-1}{2}\right)^3
$$

Therefore,

$$
\boxed{P(\text{eaten})\approx0.951}
$$

**Conclusion:** At the symmetric mixed-strategy Nash equilibrium, each tiger independently attempts to eat with probability $63.4\%$, resulting in a $95.1\%$ probability that the sheep gets eaten.
