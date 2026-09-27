# Base Rate Neglect

THe key idea is that accuracy of something ( in any direction ), cannot alone prove anything without the base rate.

## Taxi Cab

A city has two taxi companies: 85% of taxis are green and 15% are blue. A hit-and-run occurs at night, and a witness says the taxi was blue. Tests show that the witness identifies taxi colors correctly 80% of the time.
What is the probability that the taxi was actually blue?

### Solution

The formulation and the information shared in the problem make it harder to miss as you are supposed to use all the info
right, but otherwise, in the wild it's easy to miss.

$B=\text{taxi is blue},\; G=\text{taxi is green},\; W=\text{witness says blue}$
$P(B)=0.15,\; P(G)=0.85$
$P(W\mid B)=0.8,\; P(W\mid G)=0.2$
$P(B\mid W)=\frac{P(W\mid B)P(B)}{P(W\mid B)P(B)+P(W\mid G)P(G)}$
$=\frac{(0.8)(0.15)}{(0.8)(0.15)+(0.2)(0.85)}=\frac{0.12}{0.29}\approx0.414$
$\boxed{P(B\mid W)\approx41.4\%}$

Bayes' theorem incorporated the base rate accounting.

## Jurors' verdict problem

A jury has 12 members. Each juror makes the correct decision with probability $\theta$, independently. At least 8 guilty votes are needed to convict.

What is the probability that the jury reaches the correct verdict?

> The problem is incomplete unless we also know the probability that the defendant is actually guilty.

### Solution

$G=\text{defendant guilty},\; I=\text{defendant innocent},\; C=\text{jury correct}$

$P(G)=\alpha,\; P(I)=1-\alpha$

$P(C\mid G)=\sum_{i=8}^{12}\binom{12}{i}\theta^i(1-\theta)^{12-i}$

$P(C\mid I)=\sum_{i=5}^{12}\binom{12}{i}\theta^i(1-\theta)^{12-i}$

$P(C)=\alpha P(C\mid G)+(1-\alpha)P(C\mid I)$

$\boxed{\text{Without the base rate }\alpha=P(G),\;P(C)\text{ cannot be determined.}}$

### Medical test

A disease affects 1% of people. A test correctly detects the disease 95% of the time and has a 5% false-positive rate.
If a person tests positive, what is the probability they actually have the disease?

### Solution

$D=\text{has disease},\; +=\text{tests positive}$

$P(D)=0.01,\; P(+\mid D)=0.95,\; P(+\mid D^c)=0.05$

$P(D\mid +)=\frac{P(+\mid D)P(D)}{P(+\mid D)P(D)+P(+\mid D^c)P(D^c)}$

$=\frac{(0.95)(0.01)}{(0.95)(0.01)+(0.05)(0.99)}$

$=\frac{0.0095}{0.059}\approx0.161$

$\boxed{P(D\mid +)\approx16.1\%}$

## Prosecutor's fallacy

There are 10,000 equally plausible people, exactly one of whom is guilty. One person is chosen at random **before examining the DNA evidence**. The guilty person always matches the crime-scene DNA, while an innocent person has a $1/1000$ chance of matching. The chosen person matches. What is the probability they are guilty?

### Solution

$G=\text{chosen person is guilty},\; M=\text{DNA matches}$

$P(G)=\frac1{10000},\; P(M\mid G)=1,\; P(M\mid G^c)=\frac1{1000}$

$P(G\mid M)=\frac{P(M\mid G)P(G)}{P(M\mid G)P(G)+P(M\mid G^c)P(G^c)}$

$=\frac{1(0.0001)}{1(0.0001)+(0.001)(0.9999)}\approx0.091$

$\boxed{P(G\mid M)\approx9.1\%}$

**Selection matters.** An alternative problem is: if we test 10,000 people, how many DNA matches should we expect?

If one person is guilty and always matches, while each innocent person has a $1/1000$ chance of matching, then:

$E[\text{false matches}]=9999\cdot\frac{1}{1000}\approx10$

So we expect about **10 innocent matches + 1 guilty match = 11 matches total**. This is why searching a database is different from testing one preselected suspect.

> this is a bit tricky

## Fraud detection

Only 0.1% of transactions are fraudulent. A fraud detector catches 99% of frauds, but falsely flags 1% of legitimate transactions. If a transaction is flagged, what is the probability it is actually fraud?

### Solution

$F=\text{fraud},\; A=\text{flagged}$

$P(F)=0.001,\; P(A\mid F)=0.99,\; P(A\mid F^c)=0.01$

$P(F\mid A)=\frac{P(A\mid F)P(F)}{P(A\mid F)P(F)+P(A\mid F^c)P(F^c)}$

$=\frac{(0.99)(0.001)}{(0.99)(0.001)+(0.01)(0.999)}$

$=\frac{0.00099}{0.01098}\approx0.090$

$\boxed{P(F\mid A)\approx9.0\%}$

Even a 99%-sensitive detector can have low precision when fraud itself is very rare.
