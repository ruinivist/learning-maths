# Quant Level 1 — Probability and Statistics

> Best-effort semantic transcription of the main cluster in `quant-lvl1.rnote`.
> The separate hypothesis-testing cluster is intentionally omitted. Incomplete
> thoughts from the source are kept as notes or TODOs instead of being silently
> replaced by a polished formula sheet.

## Distributions

### Binomial distribution

A binomial trial has only two outcomes:

- success, with probability $p$;
- failure, with probability $q=1-p$.

The trials are independent. If $X$ is the number of successes in $n$ trials,

$$
P(X=x)=\binom{n}{x}p^xq^{n-x},
$$

and the notation is

$$
X\sim B(n,p).
$$

This is a PMF (probability mass function): it gives the probability that a
discrete random variable takes the value $x$.

More generally, for a discrete random variable,

$$
E[g(X)]=\sum_x P(X=x)g(x).
$$

#### Deriving the mean

Start directly from the definition:

$$
\begin{aligned}
E[X]
&=\sum_{k=0}^n kP(X=k)\\
&=\sum_{k=0}^n k\binom{n}{k}p^kq^{n-k}.
\end{aligned}
$$

The $k=0$ term vanishes. The useful combinatorial identity is

$$
\begin{aligned}
k\binom{n}{k}
&=k\frac{n!}{k!(n-k)!}\\
&=\frac{n!}{(k-1)!(n-k)!}\\
&=n\binom{n-1}{k-1}.
\end{aligned}
$$

Therefore,

$$
\begin{aligned}
E[X]
&=n\sum_{k=1}^n\binom{n-1}{k-1}p^kq^{n-k}\\
&=np\sum_{k=1}^n\binom{n-1}{k-1}p^{k-1}q^{n-k}.
\end{aligned}
$$

Set $j=k-1$:

$$
\begin{aligned}
E[X]
&=np\sum_{j=0}^{n-1}\binom{n-1}{j}p^jq^{(n-1)-j}\\
&=np(p+q)^{n-1}\\
&=np.
\end{aligned}
$$

The sum becomes $1$ because $p+q=1$.

#### Deriving the variance

Use

$$
\operatorname{Var}(X)=E[X^2]-E[X]^2.
$$

First find the second moment:

$$
E[X^2]=\sum_{k=0}^n k^2\binom{n}{k}p^kq^{n-k}.
$$

Again use $k\binom{n}{k}=n\binom{n-1}{k-1}$:

$$
\begin{aligned}
E[X^2]
&=np\sum_{k=1}^n k\binom{n-1}{k-1}p^{k-1}q^{n-k}\\
&=np\sum_{j=0}^{n-1}(j+1)\binom{n-1}{j}p^jq^{(n-1)-j}.
\end{aligned}
$$

Split the sum:

$$
\begin{aligned}
E[X^2]
&=np\left[
\sum_{j=0}^{n-1}j\binom{n-1}{j}p^jq^{(n-1)-j}
+
\sum_{j=0}^{n-1}\binom{n-1}{j}p^jq^{(n-1)-j}
\right]\\
&=np\bigl((n-1)p+1\bigr).
\end{aligned}
$$

The first sum is the mean of a $B(n-1,p)$ variable, and the second sum is
$(p+q)^{n-1}=1$. Hence

$$
\begin{aligned}
\operatorname{Var}(X)
&=np\bigl((n-1)p+1\bigr)-(np)^2\\
&=np(np-p+1)-n^2p^2\\
&=np(1-p)\\
&=npq.
\end{aligned}
$$

### Special cases related to the binomial

#### Bernoulli distribution

The Bernoulli distribution is the $n=1$ case:

$$
X\sim\operatorname{Bernoulli}(p).
$$

#### Geometric distribution

The geometric distribution describes the trial on which the first success
occurs in a sequence of independent Bernoulli trials. To succeed for the first
time on trial $n$, the first $n-1$ trials must fail and the $n$th must succeed:

$$
\begin{aligned}
P(X=n)
&=P(F_1)P(F_2)\cdots P(F_{n-1})P(S_n)\\
&=q^{n-1}p.
\end{aligned}
$$

Thus

$$
X\sim\operatorname{Geo}(p).
$$

The note beside this asks why the random variable has such a neat structure:
the event $X=n$ has one forced pattern—fail every time before the first success,
then succeed.

### Poisson distribution as a binomial limit

Take a binomial model in the limiting regime

$$
n\to\infty,\qquad p\to0,\qquad np=\mu\text{ constant}.
$$

This is the rare-event/large-population setup. Substitute $p=\mu/n$ into the
binomial PMF:

$$
\begin{aligned}
P(X=k)
&=\binom{n}{k}p^k(1-p)^{n-k}\\
&=\binom{n}{k}\left(\frac{\mu}{n}\right)^k
  \left(1-\frac{\mu}{n}\right)^{n-k}\\
&=\frac{n(n-1)\cdots(n-k+1)}{k!}
  \frac{\mu^k}{n^k}
  \left(1-\frac{\mu}{n}\right)^n
  \left(1-\frac{\mu}{n}\right)^{-k}\\
&=\frac{\mu^k}{k!}
  \left[\frac{n}{n}\frac{n-1}{n}\cdots\frac{n-k+1}{n}\right]
  \left(1-\frac{\mu}{n}\right)^n
  \left(1-\frac{\mu}{n}\right)^{-k}.
\end{aligned}
$$

For fixed $k$, as $n\to\infty$,

$$
\left[\frac{n}{n}\frac{n-1}{n}\cdots\frac{n-k+1}{n}\right]\to1,
\qquad
\left(1-\frac{\mu}{n}\right)^n\to e^{-\mu},
\qquad
\left(1-\frac{\mu}{n}\right)^{-k}\to1.
$$

Therefore,

$$
P(X=k)=\frac{\mu^ke^{-\mu}}{k!},
\qquad
X\sim\operatorname{Poisson}(\mu).
$$

The binomial mean and variance also converge:

$$
E[X]=np=\mu,
$$

and

$$
\operatorname{Var}(X)=np(1-p)\longrightarrow np=\mu.
$$

For a Poisson process, $\lambda$ is the average event rate. Over an interval of
length $t$, the expected number of events is

$$
\mu=\lambda t.
$$

The note's modeling intuition is: rare events in a large population lead to a
Poisson count.

### Exponential distribution from a Poisson process

If the number of events in a fixed interval is Poisson, then the waiting time
between events is exponential:

$$
T\sim\operatorname{Exp}(\lambda),
$$

where $\lambda$ is the average rate of occurrence; equivalently, the mean
waiting time is $1/\lambda$.

For a Poisson process,

$$
P(N(t)=k)=e^{-\lambda t}\frac{(\lambda t)^k}{k!}.
$$

The event that a waiting time $T$ is at most $t$ means that at least one event
has occurred by time $t$. Its CDF is therefore

$$
\begin{aligned}
P(T\le t)
&=1-P(N(t)=0)\\
&=1-e^{-\lambda t}.
\end{aligned}
$$

Differentiate the CDF (the fundamental theorem of calculus in reverse) to get
the density:

$$
f_T(t)=
\begin{cases}
\lambda e^{-\lambda t}, & t\ge0,\\
0, & t<0.
\end{cases}
$$

The survival probability is

$$
P(T>t)=e^{-\lambda t}.
$$

#### Memorylessness

The exponential distribution is memoryless:

$$
P(T>t+s\mid T>s)=P(T>t).
$$

The note's example: after something has already lasted 100 hours, its chance of
lasting another 50 hours is the same as its original chance of lasting 50
hours.

#### Hazard-rate reasoning

The chance of an occurrence during the next tiny interval $dt$, conditional on
surviving until $t$, is

$$
\begin{aligned}
P(T\le t+dt\mid T>t)
&=1-P(T>t+dt\mid T>t)\\
&=1-P(T>dt) && \text{(memorylessness)}\\
&=P(T\le dt)\\
&=1-e^{-\lambda dt}\\
&\approx \lambda dt,
\end{aligned}
$$

using the first-order Taylor approximation. The unconditional chance of failure
in $(t,t+dt]$ is survival up to $t$ times instantaneous failure after $t$:

$$
\begin{aligned}
P(t<T\le t+dt)
&=P(T>t)P(T\le dt)\\
&\approx e^{-\lambda t}\lambda dt.
\end{aligned}
$$

### Gamma distribution

The exponential distribution gives the waiting time to one event in a Poisson
process. The waiting time to the $r$th event has a gamma distribution:

$$
X\sim\operatorname{Gamma}(r,\lambda).
$$

The source leaves the detailed derivation as a TODO, with the intended use:
modeling the accumulated waiting time in a Poisson/exponential process.

### Normal distribution

For a normal random variable,

$$
X\sim N(\mu,\sigma^2),
$$

with density

$$
f_X(x)=\frac{1}{\sqrt{2\pi}\sigma}
\exp\left[-\frac{(x-\mu)^2}{2\sigma^2}\right].
$$

The expression

$$
\frac{x-\mu}{\sigma}
$$

measures how many standard deviations $x$ is from the mean. For the standard
normal distribution, $\mu=0$ and $\sigma=1$.

For a continuous variable,

$$
P(X=k)=0
$$

because a single point has zero area. The density only gives probability after
it is integrated over a range.

The cumulative distribution function is usually denoted $\Phi$ for the
standard normal:

$$
\Phi(k)=P(X\le k)=\int_{-\infty}^{k}f_X(x)\,dx.
$$

For example,

$$
P(-1\le X\le1)=\Phi(1)-\Phi(-1).
$$

Notation used in the sheet:

- lowercase $f$ for a PDF;
- uppercase $F$ for a CDF.

#### Normalization / z-transform

If $X$ is normal with mean $\mu$ and standard deviation $\sigma$, then

$$
Z=\frac{X-\mu}{\sigma}
$$

has the standard normal distribution. The note calls this a z-transform: it
converts another normal distribution into the standard normal.

### Functions of a random variable

The note's main point is that a density cannot in general be transformed by
plain substitution. Start with the CDF, then differentiate.

If $Y=g(X)$,

$$
F_Y(y)=P(Y\le y).
$$

For the linear example $Y=aX+b$, assuming $a>0$,

$$
\begin{aligned}
F_Y(y)
&=P(Y\le y)\\
&=P(aX+b\le y)\\
&=P\left(X\le\frac{y-b}{a}\right)\\
&=F_X\left(\frac{y-b}{a}\right)\\
&=F_X(g^{-1}(y)).
\end{aligned}
$$

Now differentiate:

$$
\begin{aligned}
f_Y(y)
&=\frac{d}{dy}F_Y(y)\\
&=\frac{d}{dy}F_X(g^{-1}(y)).
\end{aligned}
$$

For a monotone differentiable transformation this becomes

$$
f_Y(y)=f_X(g^{-1}(y))
\left|\frac{d}{dy}g^{-1}(y)\right|.
$$

The sheet marks the Jacobian and general multivariable transformation rule as a
TODO, together with transforming normal distributions to standard normal.

### Chi-square distribution

If

$$
Z\sim N(0,1),
$$

then

$$
Y=Z^2\sim\chi_1^2.
$$

For $k$ independent standard-normal variables,

$$
\chi_k^2=\sum_{i=1}^{k}Z_i^2.
$$

The number $k$ is the number of degrees of freedom.

## Statistical measures

### Degrees of freedom

For a system of $n$ variables, the degrees of freedom ask: how many values can
vary independently?

Example: if five variables must have a fixed mean $m$, only four can be chosen
independently. Once four are known, the fifth is forced by the mean constraint.

The loose rule written in the notes is

$$
\text{degrees of freedom}
=\text{number of variables}-\text{number of constraints}.
$$

The sheet flags this as a useful but somewhat non-mathematical-looking working
definition.

### Population measures

For a whole population $x_1,\ldots,x_N$, the mean is

$$
\mu=\frac{1}{N}\sum_{i=1}^{N}x_i.
$$

The population variance and standard deviation are

$$
\sigma^2=\frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2,
$$

$$
\sigma=\sqrt{\frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2}.
$$

The mean absolute deviation is

$$
\operatorname{MAD}=\frac{1}{N}\sum_{i=1}^{N}|x_i-\mu|.
$$

These are connected in the sheet to vector norms. For two vectors $A$ and $B$,

$$
\|A-B\|_1=\sum_i|A_i-B_i|
$$

is the Manhattan distance, while

$$
\|A-B\|_2=\sqrt{\sum_i(A_i-B_i)^2}
$$

is the Euclidean distance. MAD uses absolute distances; standard deviation uses
squared Euclidean-style distances.

### Samples and estimators

A sample is a subset of the population, used to estimate population
quantities. For a sample $X_1,\ldots,X_n$, the sample mean is

$$
\bar X=\frac{1}{n}\sum_{i=1}^{n}X_i.
$$

The sheet distinguishes two situations:

- if the listed values are the whole population, divide by the population size;
- if they are a sample used to estimate population variance, use Bessel's
  correction.

The corrected sample variance is

$$
s^2=\frac{1}{n-1}\sum_{i=1}^{n}(X_i-\bar X)^2.
$$

The reason for $n-1$ is derived rather than merely stated below.

#### First algebraic identity

The variance calculated with denominator $n$ can be rewritten as

$$
\begin{aligned}
\frac{1}{n}\sum_{i=1}^{n}(X_i-\bar X)^2
&=\frac{1}{n}\sum_{i=1}^{n}
  \left(X_i^2-2X_i\bar X+\bar X^2\right)\\
&=\frac{1}{n}\left(
  \sum_iX_i^2-2\bar X\sum_iX_i+\sum_i\bar X^2
  \right)\\
&=\frac{1}{n}\left(
  \sum_iX_i^2-2n\bar X^2+n\bar X^2
  \right)\\
&=\frac{1}{n}\sum_iX_i^2-\bar X^2.
\end{aligned}
$$

This mirrors the population identity

$$
\operatorname{Var}(X)=E[X^2]-E[X]^2.
$$

#### The sample mean is unbiased

Assume the $X_i$ are independent and identically distributed with

$$
E[X_i]=\mu,
\qquad
\operatorname{Var}(X_i)=\sigma^2.
$$

Then

$$
\begin{aligned}
E[\bar X]
&=E\left[\frac{1}{n}\sum_iX_i\right]\\
&=\frac{1}{n}\sum_iE[X_i]\\
&=\frac{1}{n}(n\mu)\\
&=\mu.
\end{aligned}
$$

So the sample mean estimates the population mean without bias.

#### Variance of the sample mean

The sheet expands this rather than jumping straight to the result:

$$
\begin{aligned}
\operatorname{Var}(\bar X)
&=E[(\bar X-E[\bar X])^2]\\
&=\frac{1}{n^2}E\left[
\left(\sum_i(X_i-\mu)\right)^2
\right]\\
&=\frac{1}{n^2}E\left[
\sum_i(X_i-\mu)^2
+\sum_{i\ne j}(X_i-\mu)(X_j-\mu)
\right].
\end{aligned}
$$

For the diagonal terms,

$$
E[(X_i-\mu)^2]=\sigma^2,
$$

so $n$ of them contribute $n\sigma^2$. For $i\ne j$, independence gives

$$
\begin{aligned}
E[(X_i-\mu)(X_j-\mu)]
&=E[X_i-\mu]E[X_j-\mu]\\
&=0.
\end{aligned}
$$

Hence

$$
\operatorname{Var}(\bar X)=\frac{n\sigma^2}{n^2}
=\frac{\sigma^2}{n}.
$$

An accompanying warning in the notes is that

$$
E[Y^2]\ne E[Y]^2
$$

in general. Pulling the expectation through the square would erase the very
variance being calculated.

#### Why dividing by $n$ is biased downward

From

$$
\operatorname{Var}(\bar X)
=E[\bar X^2]-E[\bar X]^2,
$$

we obtain

$$
E[\bar X^2]
=\frac{\sigma^2}{n}+\mu^2.
$$

Also,

$$
E[X_i^2]=\sigma^2+\mu^2.
$$

Take expectations in the earlier identity:

$$
\begin{aligned}
E\left[\frac{1}{n}\sum_i(X_i-\bar X)^2\right]
&=E\left[\frac{1}{n}\sum_iX_i^2-\bar X^2\right]\\
&=(\sigma^2+\mu^2)
  -\left(\frac{\sigma^2}{n}+\mu^2\right)\\
&=\frac{n-1}{n}\sigma^2.
\end{aligned}
$$

So the denominator-$n$ sample variance is expected to be slightly too small.
Multiplying it by $n/(n-1)$ corrects the bias:

$$
\frac{n}{n-1}\left[
\frac{1}{n}\sum_i(X_i-\bar X)^2
\right]
=\frac{1}{n-1}\sum_i(X_i-\bar X)^2.
$$

This is Bessel's correction. The source's intuition is that the population
variance is a fixed quantity, but a variance centered on the sample's own mean
is expected to come out smaller. The correction tends to $1$ as $n$ becomes
large.

### Covariance and correlation

Covariance is the average product of the two variables' deviations from their
means:

$$
\operatorname{Cov}(X,Y)
=E[(X-E[X])(Y-E[Y])].
$$

Expanding it gives

$$
\begin{aligned}
\operatorname{Cov}(X,Y)
&=E[XY-XE[Y]-YE[X]+E[X]E[Y]]\\
&=E[XY]-E[X]E[Y]-E[Y]E[X]+E[X]E[Y]\\
&=E[XY]-E[X]E[Y].
\end{aligned}
$$

Correlation normalizes covariance by both standard deviations:

$$
\rho_{X,Y}
=\frac{\operatorname{Cov}(X,Y)}{\sigma_X\sigma_Y}.
$$

### Joint probability mass functions

The sheet labels this “PDFs and JPDFs,” but the displayed example is discrete,
so it is a joint PMF. A joint PMF assigns a probability to every pair:

$$
p(x,y)=P(X=x,Y=y).
$$

It must satisfy

$$
p(x,y)\ge0
$$

for every pair and

$$
\sum_x\sum_y p(x,y)=1.
$$

The handwritten table is an example of placing one such probability at each
row/column combination of $x$ and $y$.

### Coefficient of variation

Standard deviation has units. Dividing by the mean produces a unitless relative
measure of dispersion:

$$
CV=\frac{\sigma}{\mu}.
$$

The question this answers is: how large is the standard deviation relative to
the mean?

### Outlier handling

- **Trimmed:** discard observations in the extreme tails.
- **Winsorized:** do not discard them; replace each extreme observation with
  the nearest retained boundary value.
- **Box-and-whisker plot:** displays the median, quartiles, whiskers, extremes,
  and individual outlying observations.

### Target semideviation

To study only downside risk or upside potential, choose a target $T$ and retain
only the relevant side of the population/sample:

$$
x_i<T
\qquad\text{or}\qquad
x_i>T.
$$

Then use the variance/deviation of those observations to measure downside risk
or upside potential instead of treating both sides symmetrically.

### Skewness

Skewness records asymmetry. In the pictured positively skewed distribution, the
negative/left side is compressed while the positive/right side is stretched
out into a long tail. The reverse holds for negative skew.

The pictured mean/median/mode ordering is

$$
\text{negative skew: }\text{mean}<\text{median}<\text{mode},
$$

$$
\text{symmetric: }\text{mean}=\text{median}=\text{mode},
$$

and

$$
\text{positive skew: }\text{mode}<\text{median}<\text{mean}.
$$

### Central moments

The $n$th central moment is

$$
\mu_n=E[(X-\mu)^n].
$$

The first four are interpreted in the notes as follows:

$$
\mu_1=0,
$$

$$
\mu_2=\sigma^2
\qquad\text{(variance; dispersion)},
$$

$$
\mu_3
\qquad\text{(skewness; asymmetry)},
$$

and

$$
\mu_4
\qquad\text{(kurtosis / tailedness)}.
$$

The raw moments have units raised to powers. Standardize them by $\sigma^n$ to
remove units. In particular,

$$
\gamma_1=\frac{\mu_3}{\sigma^3}
$$

is the coefficient of skewness, and

$$
\beta_2=\frac{\mu_4}{\sigma^4}
$$

is kurtosis. The note explicitly rejects using $\mu_2/\sigma^2$ as a measure:
it is always $1$.

For a normal distribution,

$$
\text{skewness}=0,
\qquad
\text{kurtosis}=3.
$$

Therefore comparisons often use excess kurtosis:

$$
\text{excess kurtosis}=\text{kurtosis}-3.
$$

The diagrams distinguish:

- **mesokurtic:** the normal benchmark, excess kurtosis $0$;
- **leptokurtic:** positive excess kurtosis, associated in the notes with a
  sharper/compressed peak and fatter tails;
- **platykurtic:** negative excess kurtosis, flatter and more spread out around
  the peak.

### Compounding returns — side note

The sheet includes a short caveat about a long list of stock returns: work with
multiplicative growth factors, not by simply adding returns. The total return is

$$
(1+r_1)(1+r_2)\cdots(1+r_n)-1,
$$

and the constant per-period geometric return is

$$
\left[(1+r_1)(1+r_2)\cdots(1+r_n)\right]^{1/n}-1.
$$

The handwritten takeaway is: **always work with the multiples**.
