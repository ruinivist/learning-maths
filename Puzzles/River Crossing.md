# River crossing

A, B, C and D need to cross a river. Each one takes a, b, c, d mins to cross individually.
But it's dark and only two can cross at one together with a torch, moving at the speed of the
slower person in the group.
How much time will it take?

## Solution

This is perhaps as clear of an example problem I've seen for "properties of the optimal solution".

Let's think of the optimal solution, and try to be better than bruter force.
Who is the problem here? Slow people for they will reduce the overall speed.

**You NEVER want to send them back**.

So now there are two choices, they either go together ( the slowest ones ) OR you have a fast
shuttle guy accompanying each slow one.

Assume ( these are times, not speeds )

$$
a \ge b \ge c \ge d
$$

### 1. Slowest together

| Step | Crossing          | Time |
| ---- | ----------------- | ---- |
| 1    | $c,d \rightarrow$ | $c$  |
| 2    | $d \leftarrow$    | $d$  |
| 3    | $a,b \rightarrow$ | $a$  |
| 4    | $c \leftarrow$    | $c$  |
| 5    | $c,d \rightarrow$ | $c$  |

$$
T_{\text{slowest together}} = a + 3c + d
$$

### 2. Fast shuttle

| Step | Crossing          | Time |
| ---- | ----------------- | ---- |
| 1    | $a,d \rightarrow$ | $a$  |
| 2    | $d \leftarrow$    | $d$  |
| 3    | $b,d \rightarrow$ | $b$  |
| 4    | $d \leftarrow$    | $d$  |
| 5    | $c,d \rightarrow$ | $c$  |

$$
T_{\text{fast shuttle}} = a+b+c+2d
$$

### Minimum time

$$
T_{\min} = \min(a+3c+d,\ a+b+c+2d)
$$

For $a=10$, $b=5$, $c=2$, $d=1$:

$$
T_{\text{slowest together}} = 10+3(2)+1=17
$$

$$
T_{\text{fast shuttle}} = 10+5+2+2(1)=19
$$

$$
\boxed{T_{\min}=17\text{ minutes}}
$$
