# Intuition and structure of the formula

## Prerequisite: standardizing a random variable

Given $X$ with mean $\mu$ and standard deviation $\sigma>0$, how do we get mean $0$ and standard deviation $1$?

First, subtract the mean. Let $Y=X-\mu$. Then

$$
E[Y]=E[X-\mu]=E[X]-\mu=0.
$$

This centers the values at $0$ without changing the variance:

$$
\operatorname{Var}(Y)=\operatorname{Var}(X-\mu)=\operatorname{Var}(X)=\sigma^2.
$$

Next, scale: let $Z=aY$ and require variance $1$:

$$
\operatorname{Var}(Z)=\operatorname{Var}(aY)=a^2\operatorname{Var}(Y)=a^2\sigma^2=1.
$$

Choosing $a=1/\sigma$ gives

$$
Z=\frac{X-\mu}{\sigma}.
$$

The **z-score** $z=(x-\mu)/\sigma$ tells us how many standard deviations $x$ lies above or below the mean. If $\mu=10$ and $\sigma=2$, then $x=14$ becomes $z=2$.

For data $x_1,\ldots,x_n$, use $z_i=(x_i-\bar{x})/s$, with mean $\bar{x}$ and standard deviation $s>0$. The transformed data have mean $0$ and standard deviation $1$; use the same variance convention ($n$ or $n-1$) throughout.

## Connection to the normal density

Standardization works for any variable with finite, positive variance. If $X$ is normal, $Z$ is **standard normal**:

$$
X\sim\mathcal{N}(\mu,\sigma^2)\quad\Longrightarrow\quad Z=\frac{X-\mu}{\sigma}\sim\mathcal{N}(0,1).
$$

Standardization alone does not make a non-normal distribution normal.

The standard normal density is

$$
\phi(z)=\frac{1}{\sqrt{2\pi}}e^{-z^2/2}.
$$

- $\frac{1}{\sqrt{2\pi}}$ is the normalization factor that makes the total area $1$.
- $e^{-z^2/2}$ gives exponential falloff in the squared distance from the center: $z$ measures distance from the mean in standard deviations, so the density falls equally on both sides.

We take the standard normal density and substitute $z=\frac{x-\mu}{\sigma}$. Dividing by $\sigma$ to keep the total area equal to $1$ gives

$$
f_X(x)=\frac{1}{\sigma}\phi\!\left(\frac{x-\mu}{\sigma}\right)=\frac{1}{\sigma\sqrt{2\pi}}\exp\!\left[-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2\right].
$$

Capital $\Phi$ is the standard normal CDF: $\Phi(z)=P(Z\le z)=\int_{-\infty}^{z}\phi(t)\,dt$. It has no closed form in elementary functions, so we use numerical methods or tables.

## Problem - Standardisation

Suppose $X\sim\mathcal{N}(10,4)$. Find $P(8\le X\le14)$.

Given: $\Phi(2)=0.9772$ and $\Phi(-1)=0.1587$.

<details>
<summary>Solution</summary>

Here $\mu=10$ and $\sigma=\sqrt{4}=2$. Standardizing gives

$$
P(8\le X\le14)=P\!\left(\frac{8-10}{2}\le Z\le\frac{14-10}{2}\right)=P(-1\le Z\le2).
$$

$$
\Phi(2)-\Phi(-1)=0.9772-0.1587=\boxed{0.8185}.
$$

The probability is approximately **81.85%**.

</details>

## Problem - Linear transform

Suppose $X\sim\mathcal{N}(3,4)$ and $Y=2X+5$. Find the mean, variance, and distribution of $Y$.

<details>
<summary>Solution</summary>

By linearity of expectation,

$$
E[Y]=E[2X+5]=2E[X]+5=2(3)+5=11.
$$

For variance, adding a constant has no effect, and multiplying by $2$ multiplies the variance by $2^2$:

$$
\operatorname{Var}(Y)=\operatorname{Var}(2X+5)=2^2\operatorname{Var}(X)=4(4)=16.
$$

A linear transformation of a normal variable is normal, so $\boxed{Y\sim\mathcal{N}(11,16)}$.

</details>

## Problem - Sum and difference

Suppose $X,Y\sim\mathcal{N}(0,1)$ independently. Find the distributions of $X+Y$ and $X-Y$.

<details>
<summary>Solution</summary>

By linearity of expectation,

$$
E[X+Y]=E[X]+E[Y]=0,\qquad E[X-Y]=E[X]-E[Y]=0.
$$

Independence makes the covariance zero, so the variances add in both cases:

$$
\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)=1+1=2.
$$

$$
\operatorname{Var}(X-Y)=\operatorname{Var}(X)+(-1)^2\operatorname{Var}(Y)=1+1=2.
$$

**Linear combinations of independent normal variables are normal** (skipping the proof). Hence

$$
\boxed{X+Y\sim\mathcal{N}(0,2)},\qquad \boxed{X-Y\sim\mathcal{N}(0,2)}.
$$

</details>
