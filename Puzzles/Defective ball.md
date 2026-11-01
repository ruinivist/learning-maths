# Defective ball

There are 12 balls, and exactly one is defective: it may be heavier or lighter than the others. Using a balance scale, identify the ball and whether it is heavy or light in at most three weighings.

## Model

Each weighing has three outcomes: the left pan is heavier, the right pan is heavier, or the pans balance. For each ball there are two hypotheses, such as `1L` (ball 1 is light) and `1H` (ball 1 is heavy). So there are $12 \times 2 = 24$ hypotheses.

Three weighings can produce $3^3=27$ outcome sequences, so there are enough outcomes in principle. But each grouping must also come from a physically possible weighing, with the same number of balls on both pans ( else your scales give no valuable information over normal balls )

## First weighing

Weigh balls 1–4 against balls 5–8; leave 9–12 aside.

| Outcome       | Remaining hypotheses                   |
| ------------- | -------------------------------------- |
| Left heavier  | `1H, 2H, 3H, 4H, 5L, 6L, 7L, 8L`       |
| Right heavier | `1L, 2L, 3L, 4L, 5H, 6H, 7H, 8H`       |
| Balance       | `9L, 9H, 10L, 10H, 11L, 11H, 12L, 12H` |

Each outcome leaves 8 hypotheses.

## Second and third weighings

First suppose the right pan was heavier. The remaining hypotheses are `1L, 2L, 3L, 4L, 5H, 6H, 7H, 8H`. Two weighings remain, so the second must leave at most 3 hypotheses in each outcome ( so the final one can resolve them decisively ).

Leave balls 7 and 8 aside. Weigh 1, 2, 5 against 3, 4, 6. The hypotheses predict these outcomes:

| Second weighing | Remaining hypotheses |
| --------------- | -------------------- |
| Right heavier   | `1L, 2L, 6H`         |
| Left heavier    | `3L, 4L, 5H`         |
| Balance         | `7H, 8H`             |

For example, `1L` predicts that the right pan is heavier because ball 1 is on the left. The arrangement splits the hypotheses into groups of 3, 3, and 2. An arbitrary 3-against-3 weighing need not do this; it can leave too many hypotheses in one branch.

Resolve each branch with the last weighing.

## Wait, on the second step? Can I just weigh put them in any as long as I make groups of upto 3?

The groups are on the hypotheses, not the count of balls.
For example this is assignment is useless.

Count of balls is satified

- Left: 1, 2, 3
- Right: 4, 5, 6
- Aside: 7, 8

Now predict what each hypothesis would do.

| Scale result  | Hypotheses         | Count |
| ------------- | ------------------ | ----- |
| Right heavier | 1L, 2L, 3L, 5H, 6H | 5     |
| Left heavier  | 4L                 | 1     |
| Balanced      | 7H, 8H             | 2     |

So the right heavier tilt, would not distinguish enough states for us.

The easy rule to go is to try to keep the number of heavy and light balls on each pan, as close to balanced as possible.

## General bound

### 1. The theoretical bound

With $N$ balls, each potentially heavier or lighter, there are $2N$ hypotheses.

Each weighing has 3 possible outcomes, so $k$ weighings can distinguish at most $3^k$ hypotheses.

$$
\boxed{2N\leq 3^k}
$$

For $k=3$:

$$
2N\leq27\implies N\leq13
$$

But **13 balls are actually impossible**.

### 2. Why 13 balls fail

After the first weighing, 2 remain, allowing at most $3^2=9$ hypotheses per outcome.

- **4 vs 4:** If balanced, 5 balls remain, giving 10 hypotheses.
- **5 vs 5:** If unbalanced, 10 hypotheses remain.

Weighing fewer than 4 or more than 5 only makes the worst case worse.

Thus, 13 balls cannot be solved in 3 weighings.

### 3. The tighter bound

Suppose the first weighing places $a$ balls on each pan, leaving $N-2a$ aside.

| Outcome       | Hypotheses |
| ------------- | ---------- |
| Left heavier  | $2a$       |
| Right heavier | $2a$       |
| Balanced      | $2(N-2a)$  |

**All three counts are even.**

After the first weighing, each branch can distinguish at most $3^{k-1}$ hypotheses, which is odd.

Therefore, each branch can contain at most $3^{k-1}-1$ hypotheses.

$$
2N\leq3(3^{k-1}-1)
$$

$$
\boxed{N\leq\frac{3^k-3}{2}}
$$

This bound is achievable in the classical problem for $k\geq2$.

For 3 weighings:

$$
\boxed{N_{\max}=\frac{27-3}{2}=12}
$$

**Key insight:** Each of the three branches must contain an even number of hypotheses, so at least one of its odd number of available outcome sequences goes unused. This explains the subtraction of 3.
