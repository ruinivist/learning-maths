## Urn Paradox

An urn initially contains no balls. One minute before noon, 10 numbered balls are added and one is randomly removed. Half a minute before noon, another 10 balls are added and one is randomly removed. This process continues infinitely, with the time between operations halving each time.

At every step, the removed ball is chosen uniformly at random from the urn.

Question: How many balls remain in the urn at noon?

### Solution

After $n$ steps, the urn contains $9n$ balls. Thus,

$$\lim_{n\to\infty}9n=\infty.$$

One might therefore expect infinitely many balls at noon.

However, consider any particular ball, introduced at step $m$.

Its probability of surviving through step $n$ is

$$P(\text{survival})=\prod_{k=m}^{n}\frac{9k}{9k+1}.$$

Since

$$\sum_{k=m}^{\infty}\frac{1}{9k+1}=\infty,$$

the infinite product converges to zero.

Thus, every individual ball has probability zero of surviving until noon.

Since there are countably many balls,

$$P(\text{at least one ball survives}) \leq \sum_{i=1}^{\infty}P(\text{ball }i\text{ survives})=0.$$

Therefore,

$$\boxed{P(\text{urn is empty at noon})=1}$$

The paradox: The number of balls grows without bound as noon approaches, yet at noon the urn is empty with probability 1.

Key insight: The limit of the number of elements need not equal the number of elements in the limiting set.

> Apparently, these are called “supertasks.”
