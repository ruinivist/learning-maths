# Horse Race

25 horses, find top 3.

## Solution

A natural start is to make **disjoint groups** and race them, since we need to process each horse. With zero initial information, it's not like we can do much better.

So divide the 25 horses into 5 groups of 5 and race each group.

| Group A | Group B | Group C | Group D | Group E |
| ------- | ------- | ------- | ------- | ------- |
| A1      | B1      | C1      | D1      | E1      |
| A2      | B2      | C2      | D2      | E2      |
| A3      | B3      | C3      | D3      | E3      |
| A4      | B4      | C4      | D4      | E4      |
| A5      | B5      | C5      | D5      | E5      |

Each column is ordered from fastest to slowest.

**Races so far: 5**

But now, we have some **information leverage**.
Since we know the ordering within each group, knowing the ordering of the group leaders would allow us to eliminate entire groups.
So race the 5 leaders. Suppose the result is:

$$
A1 > B1 > C1 > D1 > E1
$$

Now we can eliminate horses by asking: **Can this horse still be among the top 3?**
If we already know 3 horses faster than it, the answer is no.
This gives us the following triangle of possible candidates:

| Group A | Group B | Group C |
| ------- | ------- | ------- |
| **A1**  | **B1**  | **C1**  |
| **A2**  | **B2**  |         |
| **A3**  |         |         |

For example, B3 cannot be in the top 3 because A1, B1 and B2 are all faster. Similarly, C2 is beaten by A1, B1 and C1.
So only these 6 horses can possibly be in the top 3.
Notice that we also know **A1 is the fastest, without a doubt**.

## 3. Final race

Now race the other 5:

$$
A2,\ A3,\ B1,\ B2,\ C1
$$

The first two finishers give us the remaining top 3 horses.

Notice that we have narrowed the problem down to **6 possible candidates**, rather than having to compare all 25 again. These aren't necessarily the actual top 6 ( B3 would've been a candidate otherwise).
But they are the only horses that can occupy the top 3.

So, 7 races in total.
