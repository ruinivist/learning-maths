# Last ball

> A really good one.

There are 20 blue balls and 14 red balls. Remove two balls at a time. If they are different colors, add a red ball. If they are the same color, add a blue ball.

What color is the last ball?

## Solution

The key idea is to track an invariant.

Let $B$ and $R$ be the numbers of blue and red balls.

If both are blue, $(B,R)\to(B-1,R)$.
If both are red, $(B,R)\to(B+1,R-2)$.
If they are different colors, $(B,R)\to(B-1,R)$.

The parity of the number of red balls never changes. The total number of balls decreases by one each turn, so the process ends with one ball.

Since the initial number of red balls is 14, it is even. The final red-ball count must also be even, so it cannot be 1; the last ball is blue. If the process starts with 13 red balls instead, the final red-ball count is odd, so the last ball is red.
