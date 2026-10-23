## Covariance

For random variables $X,Y$ with finite second moments,

$$\operatorname{Cov}(X,Y)=E[(X-E[X])(Y-E[Y])]=E[XY]-E[X]E[Y]$$

> to remember, relate this to the 0 covar for independence case

Positive covariance means deviations from their means tend to have the same sign; negative covariance means they tend to have opposite signs.

## Properties

For constants $a,b,c,d$:

- Symmetry: $\operatorname{Cov}(X,Y)=\operatorname{Cov}(Y,X)$.
- $\operatorname{Cov}(X,X)=\operatorname{Var}(X)$.
- $\operatorname{Cov}(X,c)=0$.
- Scaling and shifts: $\operatorname{Cov}(aX+b,cY+d)=ac\operatorname{Cov}(X,Y)$.
- Additivity: $\operatorname{Cov}(X+Y,Z)=\operatorname{Cov}(X,Z)+\operatorname{Cov}(Y,Z)$.
- Independence implies $\operatorname{Cov}(X,Y)=0$. The converse need not hold; zero covariance is called **uncorrelated**.
- $|\operatorname{Cov}(X,Y)|\leq\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}$.

For sums,

$$\operatorname{Cov}\left(\sum_i a_iX_i,\sum_j b_jY_j\right)=\sum_i\sum_j a_ib_j\operatorname{Cov}(X_i,Y_j)$$

In particular,

$$\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y)$$

$$\operatorname{Var}\left(\sum_{i=1}^nX_i\right)=\sum_{i=1}^n\operatorname{Var}(X_i)+2\sum_{i<j}\operatorname{Cov}(X_i,X_j)$$

For event indicators,

$$\operatorname{Cov}(\mathbf{1}_A,\mathbf{1}_B)=P(A\cap B)-P(A)P(B)$$

## Variance properties

For random variables with finite second moments and constants $a,b$:

- $\operatorname{Var}(X)=E[(X-E[X])^2]=E[X^2]-(E[X])^2$.
- $\operatorname{Var}(X)\geq 0$.
- $\operatorname{Var}(X)=0$ if and only if $X=E[X]$ with probability $1$.
- $\operatorname{Var}(aX+b)=a^2\operatorname{Var}(X)$: shifts do not affect variance; scaling acts quadratically.
- If $X,Y$ are uncorrelated (in particular, if independent), $\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)$.

## Covariance of independent random variables

Let $X_1,\ldots,X_n$ be independent random variables with finite second moments. Then

$$\operatorname{Cov}(X_i,X_j)=E[X_iX_j]-E[X_i]E[X_j]=\begin{cases}\operatorname{Var}(X_i) & i=j \\ 0 & i\ne j\end{cases}$$

- For $i=j$, the expression is $E[X_i^2]-(E[X_i])^2=\operatorname{Var}(X_i)$.
- For $i\ne j$, independence gives $E[X_iX_j]=E[X_i]E[X_j]$, so the covariance is $0$.
