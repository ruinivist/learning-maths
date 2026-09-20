# Counting

Best-effort transcription of `probab-and-stats.rnote`.

The source is a spatial mind map rather than a linear page. This version keeps
the questions, intermediate routes, and explanations from the sheet while
putting connected ideas next to each other. Here, `n` is the number of
elements and `r` is the number of containers.

## Quick notation from the sheet

### Choosing without replacement

$$
\binom{n}{r}
$$

This is a set of `r` elements chosen from `n` distinct elements.

### Choosing with replacement

$$
\left(\!\!\binom{n}{r}\!\!\right)
=\binom{n+r-1}{r}
$$

This is the same kind of choice, but with replacement.

### Subset numbers

$$
\left\{ {n \atop r} \right\}=S(n,r)
$$

This counts ways to divide `n` distinct elements into `r` nonempty,
indistinguishable subsets.

The source uses

$$
\left[ {n \atop r} \right]=p_r(n)
$$

for ways to divide `n` identical elements (thought of as `n` ones) into `r`
nonempty, indistinguishable subsets. Equivalently, this is the number of
integer partitions of `n` into exactly `r` positive parts.

## Organising the 12-fold way

The sheet splits the problem along three decisions:

1. Are the **elements** distinct or identical?
2. What is the mapping restriction?
   - no restriction;
   - zero or one element per container;
   - at least one element per container.
3. Are the **containers** distinguishable or indistinguishable?

That gives $2\times3\times2=12$ cases.

## The easier side: distinguishable containers

### Distinct elements

#### No restriction

The sheet's reasoning is direct:

> For each of the `n` elements, there are `r` choices.

Therefore,

$$
r^n.
$$

#### Zero or one element per container

Think sequentially:

> The first element has `r` choices, the second has `r-1`, and so on.

Equivalently, choose which `n` containers will be occupied and then arrange
the `n` distinct elements among them:

$$
\binom{r}{n}n!
=r(r-1)\cdots(r-n+1)
=\frac{r!}{(r-n)!},
\qquad n\le r.
$$

If $n>r$, the count is zero.

#### At least one element per container — “hard case 1”

The route on the sheet is:

1. Divide the `n` elements into `r` nonempty subsets. This gives
   $S(n,r)$ possibilities.
2. Those subsets are currently unlabeled, so arrange the `r` subsets among
   the `r` labeled containers. This contributes $r!$.

Hence,

$$
r!S(n,r),
\qquad n\ge r.
$$

If $r>n$, the count is zero: there are not enough elements to make every
container nonempty.

### Identical elements

#### No restriction

This is choosing with replacement: distribute `n` identical elements among
`r` labeled containers.

$$
\left(\!\!\binom{r}{n}\!\!\right)
=\binom{n+r-1}{n}
=\binom{n+r-1}{r-1}.
$$

The stars-and-bars reasoning behind this appears below.

#### Zero or one element per container

The note's route is:

> Of the `r` containers, pick `n` and place an element in each.

Because the elements are identical, there is no additional arrangement:

$$
\binom{r}{n},
\qquad n\le r.
$$

If $n>r$, the count is zero.

#### At least one element per container

First pick `r` of the identical elements and put one in each of the `r`
containers. There is only one way to do that. Now distribute the remaining
$n-r$ elements among the same `r` containers with no restriction:

$$
\left(\!\!\binom{r}{n-r}\!\!\right)
=\binom{n-1}{r-1},
\qquad n\ge r.
$$

## The hard side: indistinguishable containers

### Distinct elements

#### At least one element per container

This is exactly a partition of `n` distinct elements into `r` nonempty,
unlabeled subsets:

$$
S(n,r).
$$

#### No restriction

The sheet says to loop over how many containers are actually nonempty. If
exactly `k` are nonempty, the count is $S(n,k)$. Therefore,

$$
\sum_{k=1}^{r}S(n,k).
$$

Terms with $k>n$ are zero, so the upper limit can also be $\min(n,r)$.

#### Zero or one element per container

At most one arrangement remains because the containers are indistinguishable:

$$
\begin{cases}
1, & n\le r,\\
0, & n>r.
\end{cases}
$$

When $n\le r$, each element simply occupies its own container; permuting the
containers does not produce a new distribution.

### Identical elements

#### At least one element per container — the partition case

Dividing `n` identical ones into `r` nonempty, indistinguishable subsets is an
integer partition:

$$
p_r(n)=\left[ {n \atop r} \right].
$$

The source also describes $p_r(n)$ as the number of ways to write `n` as a
sum of `r` positive integers, where order does not matter.

#### No restriction

Again, loop over the number `k` of nonempty containers:

$$
\sum_{k=1}^{r}p_k(n)
=\sum_{k=1}^{r}\left[ {n \atop k} \right].
$$

#### Zero or one element per container

The same feasibility-only answer applies:

$$
\begin{cases}
1, & n\le r,\\
0, & n>r.
\end{cases}
$$

### The partition recurrence from the sheet

The handwritten recurrence is

$$
p_r(n)=p_{r-1}(n-1)+p_r(n-r),
$$

or, in the source notation,

$$
\left[ {n \atop r} \right]
=\left[ {n-1 \atop r-1} \right]
+\left[ {n-r \atop r} \right].
$$

It separates the partitions into two cases:

1. **A part equal to one exists.** Remove that one. The remaining `n-1`
   elements form `r-1` nonempty parts, giving $p_{r-1}(n-1)$.
2. **Every part is greater than one.** Remove one element from each of the `r`
   parts. The remaining total is `n-r`, still split into `r` nonempty parts,
   giving $p_r(n-r)$.

The boundary observations on the sheet are

$$
p_r(n)=0\quad\text{when }n<r,
\qquad p_1(1)=1.
$$

## A bit of notation: the “choose bins, not balls” insight

The sheet distinguishes

$$
\binom{n}{k}
\quad\text{(choose `k` from `n` without replacement)}
$$

from

$$
\left(\!\!\binom{n}{k}\!\!\right)
\quad\text{(choose `k` from `n` with replacement)}.
$$

The useful reframing in the note is:

> Choose bins, not balls.

Turn the `n` possible element types into `n` labeled boxes. Treat the `k`
selections as `k` identical ones. Placing those ones into the boxes records
how many times each type was selected. The problem is now: place `k` identical
objects into `n` distinct boxes.

Thus,

$$
\left(\!\!\binom{n}{k}\!\!\right)
=\binom{n+k-1}{k}
=\binom{n+k-1}{n-1}.
$$

The sheet explicitly warns that this is **not**
$\binom{n+k-1}{k-1}$. The apparent mismatch comes from swapping the roles of
“number of objects” and “number of boxes”: there are `k` objects but `n`
boxes, so there are `n-1` boundaries.

### “Why not $n^k$?”

The attempted route on the sheet is:

> For the first choice there are `n` options, for the second there are `n`
> options, and so on up to `k`. Why is the answer not $n^k$?

Because that construction produces ordered sequences. For example, choosing
type `a` and then type `b` is different from choosing `b` and then `a` in the
sequence count, but they are the same multiset.

The next attempted fix is

$$
\frac{n^k}{k!}\;?
$$

That also fails. When selections repeat, different multisets have different
numbers of orderings. A multiset such as `a,a,b` has fewer distinct orderings
than `a,b,c`, so there is no single factor of $k!$ by which every sequence can
be divided.

This is why the boxes/stars-and-bars model is the useful one.

## Ones distribution — stars and bars

The sheet starts with `n` ones, so the objects are identical, and asks for
their distribution among `r` labeled containers.

The construction is:

1. Write the `n` ones in a row.
2. Divide the row into `r` groups by placing `r-1` markers.
3. Reading from left to right, the regions between consecutive boundaries are
   the `r` labeled containers. Adjacent markers represent an empty container.

There are

$$
n+(r-1)=n+r-1
$$

positions occupied by objects and boundaries together. We can count the same
arrangements in either of two ways:

- choose the `n` positions occupied by the ones;
- choose the `r-1` positions occupied by the boundaries.

Therefore,

$$
\binom{n+r-1}{n}
=\binom{n+r-1}{r-1}.
$$

This is the derivation behind the unrestricted identical-elements,
distinct-containers case.

## Subset numbers — Stirling numbers of the second kind

The source defines

$$
\left\{ {n \atop k} \right\}=S(n,k)
$$

as the number of ways to divide `n` distinct elements into `k` nonempty,
unordered subsets.

The note then derives the recurrence by focusing on element `n`. There are two
cases.

### Case 1: element `n` is separate

Make `{n}` its own subset. The other `n-1` elements must be divided into
`k-1` subsets:

$$
S(n-1,k-1).
$$

### Case 2: element `n` is part of another subset

First divide the other `n-1` elements into `k` subsets. Then pick one of those
`k` subsets and add element `n` to it:

$$
kS(n-1,k).
$$

Adding the two disjoint cases gives

$$
S(n,k)=S(n-1,k-1)+kS(n-1,k).
$$

## Compact result of the derivations

| Elements | Containers | No restriction | Zero or one | At least one |
|---|---|---:|---:|---:|
| Distinct | Distinct | $r^n$ | $\frac{r!}{(r-n)!}$ if $n\le r$, else $0$ | $r!S(n,r)$ if $n\ge r$, else $0$ |
| Identical | Distinct | $\binom{n+r-1}{r-1}$ | $\binom{r}{n}$ if $n\le r$, else $0$ | $\binom{n-1}{r-1}$ if $n\ge r$, else $0$ |
| Distinct | Identical | $\sum_{k=1}^{r}S(n,k)$ | $1$ if $n\le r$, else $0$ | $S(n,r)$ if $n\ge r$, else $0$ |
| Identical | Identical | $\sum_{k=1}^{r}p_k(n)$ | $1$ if $n\le r$, else $0$ | $p_r(n)$ if $n\ge r$, else $0$ |
