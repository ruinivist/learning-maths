# Properties of expectation

## Problem 1: Conditional expectation of a die

Roll a fair six-sided die. Let $X$ be the outcome and $Y$ indicate an even result. Find:

1. $E[X\mid Y=1]$.
2. $E[X\mid Y=0]$.
3. $E[E[X\mid Y]]$.

<details>
<summary>Show solution</summary>

Given $Y=1$, the outcomes $2,4,6$ are equally likely. Given $Y=0$, the outcomes $1,3,5$ are equally likely:

$$E[X\mid Y=1]=\frac{2+4+6}{3}=\boxed{4},\qquad E[X\mid Y=0]=\frac{1+3+5}{3}=\boxed{3}$$

By the tower property,

$$E[E[X\mid Y]]=\frac12(4)+\frac12(3)=\boxed{\frac72}=E[X]$$

The values $2$ and $1.5$ are contributions to the unconditional mean, not the conditional means.

</details>

## Problem 2: A random number of coin tosses

Choose $N$ uniformly from $\{2,4,6\}$, then toss a fair coin $N$ times independently. Let $X$ count heads. Find $E[X]$ without finding the distribution of $X$.

<details>
<summary>Show solution</summary>

Given $N=n$, $X\sim\operatorname{Bin}(n,1/2)$, so $E[X\mid N]=N/2$. Hence

$$E[X]=E[E[X\mid N]]=\frac{E[N]}2=\frac{2+4+6}{6}=\boxed{2}$$

</details>

## Problem 3: Choosing one of two coins

Choose Coin A or Coin B with equal probability. Their heads probabilities are $0.2$ and $0.8$, respectively. Flip the selected coin twice independently, and let $X$ count heads. Find $E[X]$.

<details>
<summary>Show solution</summary>

Condition on the selected coin:

$$E[X\mid A]=2(0.2)=0.4,\qquad E[X\mid B]=2(0.8)=1.6$$

$$E[X]=\frac12(0.4)+\frac12(1.6)=\boxed{1}$$

Alternatively, write $X=I_1+I_2$, where $I_j$ indicates heads on flip $j$. Each flip has marginal heads probability $\frac12(0.2)+\frac12(0.8)=0.5$, so $E[X]=0.5+0.5=1$.

The flips are independent given the coin, but dependent when the coin is unknown. Linearity does not require independence.

</details>

## Problem 4: Waiting for the first head

Flip a fair coin independently until the first head. Let $T$ count all flips, including the final head. Find $E[T]$.

<details>
<summary>Show solution</summary>

### Geometric waiting time

$T\sim\operatorname{Geom}(1/2)$, counting the successful flip, so

$$E[T]=\frac1{1/2}=\boxed{2}$$

### First-step conditioning

Let $m=E[T]$. The first flip costs one step. A head finishes; a tail restarts the process:

$$m=1+\frac12(0)+\frac12m,\qquad \boxed{m=2}$$

</details>

## Problem 5: Updating the coin choice after a head

Choose Coin A or Coin B with equal probability. Their heads probabilities are $0.2$ and $0.8$, respectively. Flip the selected coin once and observe heads. Find the expected number of heads in three more independent flips of the same coin.

<details>
<summary>Show solution</summary>

Let $H_1$ denote heads on the first flip, and let $Z$ count heads in the next three flips.

### Bayes' rule

$$P(B\mid H_1)=\frac{P(H_1\mid B)P(B)}{P(H_1)}=\frac{0.8(0.5)}{0.8(0.5)+0.2(0.5)}=0.8$$

Thus $P(A\mid H_1)=0.2$. Given the coin, future flips are independent of the first:

$$E[Z\mid H_1]=0.2(3\cdot0.2)+0.8(3\cdot0.8)=\boxed{2.04}$$

### Ratio of moments

Let $P$ be the selected coin's heads probability. Then

$$E[P]=\frac{0.2+0.8}{2}=0.5,\qquad E[P^2]=\frac{0.2^2+0.8^2}{2}=0.34$$

Observing heads weights each possible value $p$ by $p$:

$$E[P\mid H_1]=\frac{E[P^2]}{E[P]}=0.68,\qquad E[Z\mid H_1]=3E[P\mid H_1]=\boxed{2.04}$$

</details>

## Problem 6: Variance with a random number of flips

Choose $N$ uniformly from $\{2,6\}$, then toss a fair coin $N$ times independently. Let $X$ count heads. Find $\operatorname{Var}(X)$ without finding its distribution.

<details>
<summary>Show solution</summary>

$$E[N]=4,\qquad \operatorname{Var}(N)=4,\qquad E[X]=E[N/2]=2$$

### Total variance

Given $N$, the count is binomial:

$$E[X\mid N]=\frac N2,\qquad \operatorname{Var}(X\mid N)=\frac N4$$

$$\operatorname{Var}(X)=E[\operatorname{Var}(X\mid N)]+\operatorname{Var}(E[X\mid N])=\frac{E[N]}4+\frac{\operatorname{Var}(N)}4=1+1=\boxed{2}$$

One unit comes from the flips given $N$; the other comes from the randomness in $N$.

### Factorial moments

For a binomial count, $E[X(X-1)\mid N]=N(N-1)/4$. Average over $N=2,6$:

$$E[X(X-1)]=\frac12\left(\frac{2\cdot1}{4}+\frac{6\cdot5}{4}\right)=4$$

Since $X^2=X(X-1)+X$,

$$E[X^2]=4+2=6,\qquad \operatorname{Var}(X)=6-2^2=\boxed{2}$$

</details>

## Problem 7: Waiting for two consecutive heads

Flip a fair coin independently until two consecutive heads (HH) appear. Let $T$ count all flips, including the final one. Find $E[T]$.

<details>
<summary>Show solution</summary>

### First-step conditioning

Let $A$ be the expected additional flips with no trailing head, and $B$ the expected additional flips with one trailing head.

A tail from state $A$ leaves the state unchanged; a head moves to $B$. From $B$, a head finishes and a tail returns to $A$:

$$A=1+\frac12A+\frac12B,\qquad B=1+\frac12A$$

The first equation gives $A=2+B$. Substitution yields

$$A=3+\frac A2,\qquad \boxed{E[T]=A=6},\qquad B=4$$

A tail after the first head resets the search for HH.

### Geometric attempts

An attempt consists of waiting for a head, then flipping once more. The extra flip either completes HH or ends in a tail, restarting the process.

- The expected attempt length is $2+1=3$.
- Each attempt succeeds with probability $1/2$, so the expected number of attempts is $2$.
- Attempt lengths are independent of the final-flip outcomes that determine the number of attempts.

Conditioning on the number of attempts gives

$$E[T]=E[\text{number of attempts}]\,E[\text{attempt length}]=2\cdot3=\boxed{6}$$

This also follows from Wald's identity. First-step conditioning applies to other patterns, such as HTH.

</details>

### Follow-up: Waiting for HT

Let $T_{HT}$ count flips until a head immediately followed by a tail first appears, including the final tail. Find $E[T_{HT}]$. Why does it differ from the expected waiting time of $6$ flips for HH?

<details>
<summary>Show solution</summary>

For HT, let $g_0$ be the expected waiting time from the start or after a tail, and $g_1$ the expected waiting time after a head, before HT has appeared.

For HT, once you have a head, your progress cannot be destroyed:

- Another head leaves a head at the end, so you are still one tail away from finishing.
- A tail completes HT.

From the start, a tail leaves us at $g_0$ and a head moves us to $g_1$. After a head, a tail finishes and another head leaves us at $g_1$:

$$g_0=1+\frac12g_0+\frac12g_1,\qquad g_1=1+\frac12(0)+\frac12g_1$$

Thus $g_1=2$ and $g_0=2+g_1=4$:

$$E[T_{HT}]=g_0=\boxed{4}$$

For HH, a tail after the first head destroys your progress: HT does not finish HH, and you must find a new first head. This restart makes $h_2=6$, compared with $E[T_{HT}]=4$.

Both patterns have probability $1/4$ in a fixed pair of flips. But consecutive pairs overlap and share a flip, so they are not independent attempts. Their first waiting times depend on how each new flip preserves or destroys progress.

</details>

## Problem 8: A die chooses the number of tosses

Roll a fair six-sided die to choose $N$, then toss a fair coin $N$ times independently. Let $X$ count heads. Without finding its distribution, find:

1. $E[X]$.
2. $E[X^2]$.
3. $\operatorname{Var}(X)$.

<details>
<summary>Show solution</summary>

Given $N=n$, $X\sim\operatorname{Bin}(n,1/2)$. For the die,

$$E[N]=\frac72,\qquad E[N^2]=\frac{1^2+\cdots+6^2}{6}=\frac{91}{6},\qquad \operatorname{Var}(N)=\frac{35}{12}$$

### Mean

$$E[X]=E[E[X\mid N]]=\frac{E[N]}2=\boxed{\frac74}$$

### Second moment

$$E[X^2\mid N]=\operatorname{Var}(X\mid N)+(E[X\mid N])^2=\frac N4+\frac{N^2}{4}$$

$$E[X^2]=\frac{E[N]+E[N^2]}4=\frac{7/2+91/6}{4}=\boxed{\frac{14}{3}}$$

### Variance

$$\operatorname{Var}(X)=E[X^2]-(E[X])^2=\frac{14}{3}-\left(\frac74\right)^2=\boxed{\frac{77}{48}}$$

Alternatively, total variance gives

$$\operatorname{Var}(X)=E[N/4]+\operatorname{Var}(N/2)=\frac78+\frac14\left(\frac{35}{12}\right)=\frac{77}{48}$$

</details>

## Problem 9: A uniformly random coin bias

Choose $P\sim\operatorname{Uniform}(0,1)$, then flip a coin twice with heads probability $P$. The flips are independent given $P$.

Given heads on the first flip, find the probability of heads on the second.

<details>
<summary>Show solution</summary>

Let $H_1,H_2$ denote heads on the first and second flips.

### Bayes' rule for densities

The prior density is $f_P(p)=1$ on $[0,1]$, and $P(H_1)=E[P]=1/2$. Thus

$$f_{P\mid H_1}(p)=\frac{P(H_1\mid P=p)f_P(p)}{P(H_1)}=2p,\qquad 0\leq p\leq1$$

$$P(H_2\mid H_1)=E[P\mid H_1]=\int_0^1p(2p)\,dp=\boxed{\frac23}$$

### Conditional probability

Given $P=p$, the probability of two heads is $p^2$. Therefore

$$P(H_1\cap H_2)=E[P^2]=\frac13,\qquad P(H_1)=E[P]=\frac12$$

$$P(H_2\mid H_1)=\frac{P(H_1\cap H_2)}{P(H_1)}=\frac{1/3}{1/2}=\boxed{\frac23}$$

The flips are independent given $P$, but dependent after averaging over $P$.

</details>

## Problem 10: A random sum of die rolls

Roll a fair six-sided die to choose $N$. Independently of $N$, roll a fair die $N$ times, obtaining independent outcomes $X_1,\ldots,X_N$. Let $S=\sum_{i=1}^N X_i$. Without finding its distribution, find:

1. $E[S]$.
2. $\operatorname{Var}(S)$.

<details>
<summary>Show solution</summary>

Each roll, including the initial die, has mean $\mu=7/2$ and variance $\sigma^2=35/12$.

### Mean

$$E[S\mid N]=N\mu=\frac72N,\qquad E[S]=\frac72E[N]=\boxed{\frac{49}{4}}$$

### Variance

Given $N$, the roll variances add:

$$\operatorname{Var}(S\mid N)=N\sigma^2=\frac{35}{12}N$$

By total variance,

$$\operatorname{Var}(S)=E[\operatorname{Var}(S\mid N)]+\operatorname{Var}(E[S\mid N])=\frac{35}{12}E[N]+\frac{49}{4}\operatorname{Var}(N)=\frac{245}{24}+\frac{1715}{48}=\boxed{\frac{735}{16}}$$

### Check using the second moment

$$E[S^2\mid N]=\operatorname{Var}(S\mid N)+(E[S\mid N])^2=\frac{35}{12}N+\frac{49}{4}N^2$$

Using $E[N^2]=91/6$,

$$E[S^2]=\frac{35}{12}\cdot\frac72+\frac{49}{4}\cdot\frac{91}{6}=196,\qquad \operatorname{Var}(S)=196-\left(\frac{49}{4}\right)^2=\frac{735}{16}$$

</details>

## Problem 11: Waiting for red after changing an urn

A box contains 3 red and 2 blue balls. Flip a fair coin:

- On heads, add 2 red balls.
- On tails, add 2 blue balls.

Draw independently and uniformly with replacement until a red ball appears. Let $T$ count draws. Find $E[T]$.

<details>
<summary>Show solution</summary>

Let $H$ denote heads on the initial coin flip. Given the box contents, $T$ is geometric:

$$E[T\mid H]=\frac1{5/7}=\frac75,\qquad E[T\mid H^c]=\frac1{3/7}=\frac73$$

By the tower property,

$$E[T]=\frac12\cdot\frac75+\frac12\cdot\frac73=\boxed{\frac{28}{15}}$$

More generally, if a success probability $P>0$ is chosen once and the trials are independent given $P$, then $E[T\mid P]=1/P$ and $E[T]=E[1/P]$. This expectation may be infinite.

</details>

## Problem 12: Expected number of distinct die faces

Choose $N$ uniformly from $\{2,4\}$, then roll a fair die $N$ times independently. Let $X$ count distinct faces observed. Find $E[X]$ without enumerating sequences.

<details>
<summary>Show solution</summary>

Let $I_i$ indicate that face $i$ appears at least once. Then $X=\sum_{i=1}^6I_i$. Given $N=n$, face $i$ is absent with probability $(5/6)^n$, so

$$E[I_i\mid N=n]=1-\left(\frac56\right)^n,\qquad E[X\mid N=n]=6\left[1-\left(\frac56\right)^n\right]$$

Average over $N=2,4$:

$$E[X]=\frac12\cdot6\left[1-\left(\frac56\right)^2\right]+\frac12\cdot6\left[1-\left(\frac56\right)^4\right]=\frac12\left(\frac{11}{6}+\frac{671}{216}\right)=\boxed{\frac{1067}{432}}$$

The indicators need not be independent for their expectations to add.

</details>

## Problem 13: Conditioning on the sum of two dice

Roll two independent fair six-sided dice. Let $X,Y$ be their outcomes and $S=X+Y$. Without listing all 36 ordered outcomes, find:

1. $E[X\mid S]$ as a function of $S$.
2. $E[XS]$.

<details>
<summary>Show solution</summary>

### Symmetry and the tower property

The dice are exchangeable, so $E[X\mid S]=E[Y\mid S]$. Also,

$$E[X\mid S]+E[Y\mid S]=E[X+Y\mid S]=S,\qquad \boxed{E[X\mid S]=\frac S2}$$

When conditioning on $S$, the factor $S$ is known:

$$E[XS]=E[E[XS\mid S]]=E[S\,E[X\mid S]]=\frac12E[S^2]$$

Since $E[S]=7$ and $\operatorname{Var}(S)=2(35/12)=35/6$,

$$E[S^2]=\operatorname{Var}(S)+(E[S])^2=\frac{35}{6}+49=\frac{329}{6},\qquad \boxed{E[XS]=\frac{329}{12}}$$

### Conditional expectation using Bayes' rule

For $2\leq s\leq12$,

$$P(X=x\mid S=s)=\frac{P(S=s\mid X=x)P(X=x)}{P(S=s)}$$

The numerator is $1/36$ when $1\leq x\leq6$ and $1\leq s-x\leq6$, and zero otherwise. Thus the valid values of $X$ are uniformly distributed over the integers from $a$ to $b$, where

$$a=\max(1,s-6),\qquad b=\min(6,s-1)$$

Since $a+b=s$,

$$E[X\mid S=s]=\frac{a+b}{2}=\boxed{\frac s2}$$

Use the tower-property calculation above to find $E[XS]$.

### Direct calculation of $E[XS]$

Independence gives $E[XY]=E[X]E[Y]$, so

$$E[XS]=E[X(X+Y)]=E[X^2]+E[X]E[Y]=\frac{91}{6}+\frac72\cdot\frac72=\boxed{\frac{329}{12}}$$

</details>

## Problem 14: Bidding for a mystery prize

A mystery prize has value $V\sim\operatorname{Uniform}(0,1)$, measured in millions of dollars. Choose a fixed bid $b\geq0$ without knowing $V$.

- If $b<2V/3$, the bid is rejected and your payoff is $0$.
- If $b\geq2V/3$, you pay $b$, receive the prize, and your payoff is $V-b$.

Find the bid that maximizes your expected payoff.

<details>
<summary>Show solution</summary>

Let $W$ be your payoff. Acceptance means $V\leq3b/2$, so an accepted bid selects prizes with lower values.

For $0<b\leq2/3$, the probability of acceptance is $3b/2$. Given acceptance, $V$ is uniform on $[0,3b/2]$, so

$$E[V\mid\text{accepted}]=\frac{3b}{4},\qquad E[W\mid\text{accepted}]=\frac{3b}{4}-b=-\frac b4$$

Rejected bids have zero payoff. By conditioning on acceptance,

$$E[W]=P(\text{accepted})E[W\mid\text{accepted}]=\frac{3b}{2}\left(-\frac b4\right)=-\frac{3b^2}{8}<0$$

For $b>2/3$, every bid is accepted, giving

$$E[W]=E[V]-b=\frac12-b<0$$

At $b=0$, the payoff is $0$ with probability $1$. Every positive bid has negative expected payoff, so

$$\boxed{b^*=0,\qquad \max E[W]=0}$$

Using the unconditional mean $E[V]=1/2$ for an accepted prize would miss the information supplied by acceptance. For positive bids up to $2/3$, an accepted prize is worth only $3b/4$ on average, less than the price $b$ you pay.

Winner's curse: expected value on conditioning the bid is expected is oftern lower than the unconditional expected value

</details>

## Problem 15: A random walk on the integers

A walker starts at $0$. At each step, independently, they move one unit left or right with equal probability. Let $b$ be a googolplex, $10^{10^{100}}$.

1. What is the probability that the walker visits $b$ before returning to $0$ for the first time?
2. What is the expected number of visits to $b$ before that first return to $0$?

<details>
<summary>Show solution</summary>

Let $A$ be the event that the walker visits $b$ before returning to $0$, and let $X_1$ be the position after the first step. Conditioning on that step,

$$P(A)=P(A\mid X_1=1)P(X_1=1)+P(A\mid X_1=-1)P(X_1=-1)$$

The fair [gambler's ruin](../Famous%20problems/Gamblers%20ruin.md) result says that a walk starting at $i$ between $0$ and $b$ reaches $b$ before $0$ with probability $i/b$. Starting from $1$, this gives $P(A\mid X_1=1)=1/b$.

Starting from $-1$, the walker must pass through $0$ before reaching $b$, so $P(A\mid X_1=-1)=0$. Each first step has probability $1/2$, giving

$$P(A)=\frac1b\cdot\frac12+0\cdot\frac12=\boxed{\frac{1}{2b}}$$

After a visit to $b$, the next step is to $b-1$ or $b+1$, each with probability $1/2$. From $b-1$, gambler's ruin gives the probability of reaching $b$ before $0$:

$$P(\text{reach }b\text{ before }0\mid X_0=b-1)=\frac{b-1}{b}$$

The walk eventually reaches one of these boundaries, so the probability of reaching $0$ before returning to $b$ is the complement:

$$P(\text{reach }0\text{ before }b\mid X_0=b-1)=1-\frac{b-1}{b}=\frac1b$$

From $b+1$, the walk must pass through $b$ before reaching $0$, so the corresponding probability is $0$. Conditioning on the next step, the probability that the current visit to $b$ is the last before returning to $0$ is

$$\frac12\cdot\frac1b+\frac12\cdot0=\frac1{2b}$$

Given that the walker reaches $b$, the number of visits to $b$ is geometric with success probability $1/(2b)$ and mean $2b$. Otherwise it is zero. Hence

$$E[\text{visits to }b]=\frac{1}{2b}\cdot 2b=\boxed{1}$$

### First-step analysis (FSA)

Use two states after a visit to $b$: either the walk returns to $b$, or it reaches $0$ and stops. Let $m$ be the expected number of visits to $b$ starting at $b$, counting the current visit. The return state has probability $1-1/(2b)$ and expected future visits $m$; the stopping state has probability $1/(2b)$ and expected future visits $0$. Thus

$$m=1+\left(1-\frac1{2b}\right)m+\frac1{2b}\cdot0$$

Solving gives $m=2b$. Conditioning on whether the walk reaches $b$ before its first return to $0$,

$$E[\text{visits to }b]=P(A)m+P(A^c)\cdot0=\frac1{2b}\cdot2b=\boxed{1}$$

</details>

## Word problems

### Problem 16: Life expectancy

Fred is 30 years old. The average lifespan in his country is 80 years. Can he conclude that his expected remaining lifespan is 50 years?

<details>
<summary>Show solution</summary>

Let $T$ be Fred's lifespan. Assuming Fred's lifespan follows the country's lifespan distribution, $E[T]=80$. Since he has reached age 30, his expected remaining lifespan is

$$E[T-30\mid T\geq30]=E[T\mid T\geq30]-30$$

The average of 80 includes people who died before age 30. By the law of total expectation, excluding them cannot lower the average lifespan. If there is a positive chance of dying before age 30, then $E[T\mid T\geq30]>80$, so Fred's expected remaining lifespan is greater than 50 years. If no one dies before age 30, it equals 50 years.

The exact expectation cannot be found from the overall average alone; it depends on the lifespan distribution.

</details>
