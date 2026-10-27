# Missing numbers

Numbers from 1 to 100. For k = 1, 2 missing, find which ones in O(n) time and O(1) space.

## Solution

The contraints are the only problem else you can easily find upto k missing with sorting in O(nlogn) time and O(1) space or with hashset in O(n) time and O(n) space.

_k=1_
is trivial, sum(expected) - sum(actual) is the result.
Any reversible binary op will work like xor.

_k=2_

Let the numbers be x and y.
x + y = sum(expected) - sum(actual)
x^2 + y^2 = squared sums(expected) - squared sums(actual)

Then you can solve the two equations and two unknowns.

You can technically do this for higher ks too but cubics are already hard to solve.
