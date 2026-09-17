# Inclusion Exclusion on sets

For \(n\) sets \(A_1,\dots,A_n\), inclusion–exclusion is

$$
\boxed{
\left|\bigcup_{i=1}^n A_i\right|
=
\sum_i |A_i|
-\sum_{i<j}|A_i\cap A_j|
+\sum_{i<j<k}|A_i\cap A_j\cap A_k|
-\cdots
+(-1)^{n+1}|A_1\cap\cdots\cap A_n|
}
$$

**There is NO factor of \(2\) on the pair terms** or higher combinations as we are working with
sets, these are unordered combinations.

A useful memory rule is:

$$
\boxed{\text{singles }+,\quad \text{pairs }-,\quad \text{triples }+,\quad \text{4-way }-,\ldots}
$$
