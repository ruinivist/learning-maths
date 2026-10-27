# Probability spaces and their relation to linear algebra

I feel like everything useful is in some manner related to linear algebra.

## The idea of a probability space

To relate probability to vectors and represent things as vectors, the idea of a probability space comes first. Measure theory distills probability down to a "measure" of something, rather than giving it an inherent meaning of "chance" (though that is the interpretation I have in mind).

A probability space is \((\Omega, \mathcal F, P)\), where \(\Omega\) is the set of possible outcomes and \(\mathcal F\) is the collection of events we can assign probabilities to. For a finite sample space, we can take \(\mathcal F = 2^\Omega\): the set of all subsets of \(\Omega\), including the empty set. More generally, \(\mathcal F\) is a sigma-algebra.

Now define \(P\) as a mapping \(P: \mathcal F \to [0,1]\). Each set in \(\mathcal F\) (some event) is assigned a number via \(P\). We also require \(P(\Omega)=1\) and the additivity rule below.

### A die example

For a roll, \(\Omega = \{1,2,3,4,5,6\}\). The events in \(\mathcal F\) are sets of outcomes. For example, if I wanted to pick "even," I would attach that word to the set \(\{2,4,6\}\), and \(P\) must be able to take that set as input and give me back a number, a "measure":

$$P(\text{even}) = P(\{2,4,6\}) = \frac{1}{2}$$

Now mapping this to vectors? Let's say the cardinality of the sample space is \(N\), so \(|\Omega|=N\). If \(\mathcal F=2^\Omega\), then \(|\mathcal F|=2^N\). Listing the probability of every event would give a \(2^N\)-dimensional vector, with one scalar for each event.

### Applying the third axiom

And this is how we reduce from exponential dimension to \(N\).

For any countable collection of mutually exclusive events,

$$P\left(\bigcup_i A_i\right) = \sum_i P(A_i).$$

This way, for a finite sample space, the probabilities of all events are determined by an \(N\)-dimensional vector: one probability for each individual outcome (or singleton event) in the sample space.

$$\mathbf p = \begin{bmatrix}P(\{w_1\})\\P(\{w_2\})\\\vdots\\P(\{w_N\})\end{bmatrix}$$

Why \(\mathcal F\), then? It's part of the definition that makes the whole idea rigorous: it tells us which subsets of the sample space we are allowed to assign probabilities to. For a finite sample space I can just use every subset. I could argue that \(\mathcal F\) isn't needed here, but apparently things like Vitali sets cause trouble in more general spaces. That's deeper measure theory, I guess.

For the rest of this discussion, and I think forever for my case, I can mostly ignore \(\mathcal F\).

## Definition of a random variable

\(X:\Omega\to\mathbb R\) maps **each outcome** in the sample space to a number. If \(w_1,w_2,\ldots,
w_N\) are the outcomes, the random-variable vector is

$$\mathbf x = \begin{bmatrix}X(w_1)\\X(w_2)\\\vdots\\X(w_N)\end{bmatrix}$$

In other words, it says what number to emit when each outcome occurs. For a die, if \(X\) is "the
number rolled," then

$$\mathbf x = \begin{bmatrix}1\\2\\3\\4\\5\\6\end{bmatrix}$$

If instead \(X\) is "1 if even, 0 if odd," then

$$\mathbf x = \begin{bmatrix}0\\1\\0\\1\\0\\1\end{bmatrix}$$

Note that this is just a function, and I'm forcing it to be a vector by writing its values as
coordinates indexed by the \(N\) outcomes.

### Expectation as an inner product

Take a fair die, and let my score be the number I roll. The outcomes \(1,2,\ldots,6\) give me six
coordinates, and the random variable tells me the score at each one:

$$\mathbf x=\begin{bmatrix}1\\2\\3\\4\\5\\6\end{bmatrix}$$

The probability vector tells me where the mass is. For a fair die, every outcome has the same mass:

$$\mathbf p=\begin{bmatrix}1/6\\1/6\\1/6\\1/6\\1/6\\1/6\end{bmatrix}$$

If I put those masses at the positions given by \(X\), the expectation is their center of mass. In
vector notation, I multiply corresponding coordinates and add:

$$
\mathbb E[X]=\mathbf p^{\mathsf T}\mathbf x
=\frac{1}{6}(1+2+3+4+5+6)
=\frac{7}{2}
$$

This also makes linearity feel less mysterious. For random variables \(X\) and \(Y\) on the same
outcomes, their vectors add coordinate by coordinate, so

$$
\mathbb E[aX+bY]
=\mathbf p^{\mathsf T}(a\mathbf x+b\mathbf y)
=a\mathbb E[X]+b\mathbb E[Y]
$$

For a simpler example on that same die, let \(Y\) be \(1\) when the roll is even and \(0\) otherwise.
Its vector is

$$\mathbf y=\begin{bmatrix}0\\1\\0\\1\\0\\1\end{bmatrix}$$

If my score is the number rolled **plus** the even-roll bonus, its vector is just the sum

$$
\mathbf x+\mathbf y
=\begin{bmatrix}1\\3\\3\\5\\5\\7\end{bmatrix}
$$

The probability vector is still the same six-entry \(\mathbf p\). I don't have to change it when I add
the scores:

$$
\mathbb E[X+Y]
=\mathbf p^{\mathsf T}(\mathbf x+\mathbf y)
=\mathbb E[X]+\mathbb E[Y]
=\frac{7}{2}+\frac{1}{2}
=4
$$

\(X\) and \(Y\) are related—knowing the roll tells me whether there's a bonus—but that doesn't affect
the dot product. For this same die, \(\mathbf p\) stays fixed; only the random-variable vector changes.

## Generalising

Let \(p_i=P(\{w_i\})\). The probability-weighted inner product is

$$
\langle X,Y\rangle_P
=\mathbf x^{\mathsf T}\operatorname{diag}(\mathbf p)\mathbf y
=\sum_{i=1}^{N}p_iX(w_i)Y(w_i)
=\mathbb E[XY]
$$

In particular, with \(1(w_i)=1\),

$$\mathbb E[X]=\langle X,1\rangle_P$$

Center the random variables:

$$X_c=X-\mathbb E[X],\qquad Y_c=Y-\mathbb E[Y]$$

Then

$$
\operatorname{Var}(X)
=\langle X_c,X_c\rangle_P
=\|X_c\|_P^2
$$

$$
\operatorname{Cov}(X,Y)
=\langle X_c,Y_c\rangle_P
$$

Thus \(\operatorname{Cov}(X,Y)=0\) means \(X_c\perp Y_c\) under this inner product.

For nonzero variances,

$$
\boxed{
\rho(X,Y)
=\frac{\operatorname{Cov}(X,Y)}
{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}}
=\frac{\langle X_c,Y_c\rangle_P}
{\|X_c\|_P\|Y_c\|_P}
=\cos\theta
}
$$

If some \(p_i=0\), ignore those coordinates when defining lengths and angles.

## Some interesting bits

Covariance is bilinear:

$$
\operatorname{Cov}(aX+bY,Z)
=a\operatorname{Cov}(X,Z)+b\operatorname{Cov}(Y,Z)
$$

So variance expands like a squared length:

$$
\begin{aligned}
\operatorname{Var}(X+Y)
&=\operatorname{Cov}(X+Y,X+Y)\\
&=\operatorname{Cov}(X,X)+\operatorname{Cov}(X,Y)
 +\operatorname{Cov}(Y,X)+\operatorname{Cov}(Y,Y)\\
&=\operatorname{Var}(X)+2\operatorname{Cov}(X,Y)+\operatorname{Var}(Y)
\end{aligned}
$$

If \(X_c\perp Y_c\), then \(\operatorname{Cov}(X,Y)=0\), giving Pythagoras:

$$
\|X_c+Y_c\|_P^2
=\|X_c\|_P^2+\|Y_c\|_P^2
\quad\Longleftrightarrow\quad
\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)
$$

Remember that L2 norm^2 ( length^2 ) is inner product with self. So the length^2 aka variance is that
probab weighted self inner product.

## Conditional expectation as projection

The route is: ordinary projection, the probability-weighted geometry, then the subspace determined by the information available. Start with a finite sample space and positive outcome probabilities, so random variables are vectors as above.

### Ordinary projection: keep the part in a subspace

A subspace $S$ is a collection of vectors closed under addition and scalar multiplication. A line through the origin is one example; a plane through the origin is another.

Given a vector $x$, its orthogonal projection $m$ onto $S$ satisfies two conditions:

$$m\in S,\qquad r=x-m\perp S.$$

The residual $r$ is the error left after replacing $x$ with $m$. Being perpendicular to $S$ means $\langle r,z\rangle=0$ for every $z\in S$.

![A vector x splits into its projection m along a subspace S and a perpendicular residual r. An alternative point z in S gives a longer error by Pythagoras.](Projection%20geometry.svg)

Why does this give the closest point? For any other $z\in S$, the difference $m-z$ also lies in $S$, so it is perpendicular to $r$. Pythagoras gives

$$\|x-z\|^2=\|r+(m-z)\|^2=\|r\|^2+\|m-z\|^2.$$

The first term is fixed. Choosing $z=m$ makes the second term zero, giving the smallest distance.

For a line spanned by a nonzero vector $u$, write $m=cu$. The perpendicular-error condition determines $c$:

$$\langle x-cu,u\rangle=0\quad\Longrightarrow\quad m=\frac{\langle x,u\rangle}{\langle u,u\rangle}u.$$

### Use the probability-weighted geometry

For random variables, use the inner product from above:

$$\langle X,Z\rangle_P=\mathbb E[XZ],\qquad \|X-Z\|_P^2=\mathbb E[(X-Z)^2].$$

Distance squared is therefore the mean squared prediction error. More probable outcomes contribute more to that distance.

Even ordinary expectation has a projection interpretation. Let $\mathbf 1=(1,\ldots,1)$, so the constant random variables form the line $\{c\mathbf 1:c\in\mathbb R\}$. Since $\langle\mathbf 1,\mathbf 1\rangle_P=1$, the line-projection formula gives

$$\operatorname{proj}_{\text{constants}}X=\frac{\langle X,\mathbf 1\rangle_P}{\langle\mathbf 1,\mathbf 1\rangle_P}\mathbf 1=\mathbb E[X]\mathbf 1.$$

If you must predict using one constant, the closest prediction is the mean. Its residual is $X-\mathbb E[X]$, whose squared length is $\operatorname{Var}(X)$.

### Information determines a subspace

Take the fair die again. Let $X$ be the number rolled, and let $Y$ be $1$ for an even roll and $0$ for an odd roll:

$$X=(1,2,3,4,5,6),\qquad Y=(0,1,0,1,0,1).$$

Suppose you observe only $Y$. You cannot distinguish outcomes $1,3,5$ from one another, so a prediction using only $Y$ must give them the same value $a$. Likewise, it must give outcomes $2,4,6$ the same value $b$.

All available predictions therefore form the subspace

$$S_Y=\{g(Y):g:\{0,1\}\to\mathbb R\}=\{(a,b,a,b,a,b):a,b\in\mathbb R\}.$$

It is a subspace because adding two such vectors, or multiplying one by a scalar, preserves this pattern. It has two independent directions: the indicators of the odd and even groups.

$$e_{\mathrm{odd}}=(1,0,1,0,1,0),\qquad e_{\mathrm{even}}=(0,1,0,1,0,1),\qquad S_Y=\operatorname{span}\{e_{\mathrm{odd}},e_{\mathrm{even}}\}.$$

This is where the collection of observable events matters: it tells us which outcomes we can distinguish. For this example, grouping outcomes by $Y$ captures all the information we need.

### Conditional expectation averages within each group

Given $Y=0$, the possible rolls are $1,3,5$, with equal conditional probabilities. Given $Y=1$, they are $2,4,6$. Their conditional means are

$$\mathbb E[X\mid Y=0]=\frac{1+3+5}{3}=3,\qquad \mathbb E[X\mid Y=1]=\frac{2+4+6}{3}=4.$$

Putting those predictions back into the six outcome coordinates gives

$$M=\mathbb E[X\mid Y]=(3,4,3,4,3,4).$$

![Parity groups the die outcomes into odd and even rolls. Conditional expectation replaces each group's values with its mean; the errors sum to zero separately within each group.](Conditional%20expectation%20groups.svg)

$\mathbb E[X\mid Y=0]$ is a number. $\mathbb E[X\mid Y]$ is a random variable: its prediction depends on the observed value of $Y$. Both $X$ and $M$ still have six coordinates; only the allowed pattern of those coordinates has changed.

For unequal probabilities, use the conditional weights. If $p_i=P(\{w_i\})$ and $P(Y=y)>0$, then

$$m_y=\mathbb E[X\mid Y=y]=\frac{\sum_{i:Y(w_i)=y}p_iX(w_i)}{\sum_{i:Y(w_i)=y}p_i},\qquad M(w_i)=m_{Y(w_i)}.$$

### Why the remaining error is perpendicular

For the fair die, subtract the prediction:

$$R=X-M=(-2,-2,0,0,2,2).$$

Take any allowed prediction $Z=(a,b,a,b,a,b)\in S_Y$. Then

$$\langle R,Z\rangle_P=\frac16(-2a-2b+0a+0b+2a+2b)=0.$$

The errors cancel within each group. Every allowed prediction is constant within those groups, so multiplying by it preserves that cancellation.

The same reasoning works with unequal probabilities. The definition of each group mean gives

$$\sum_{i:Y(w_i)=y}p_i\bigl(X(w_i)-m_y\bigr)=0.$$

For any $Z=g(Y)$, group the terms in the inner product by $y$:

$$\langle X-M,g(Y)\rangle_P=\sum_y g(y)\sum_{i:Y(w_i)=y}p_i\bigl(X(w_i)-m_y\bigr)=0.$$

Thus $M\in S_Y$ and $X-M\perp S_Y$. These are exactly the two conditions for orthogonal projection:

$$\boxed{\mathbb E[X\mid Y]=\operatorname{proj}_{S_Y}X.}$$

### Why this is the best prediction using $Y$

For any competing prediction $g(Y)$, Pythagoras in the weighted geometry gives

$$\mathbb E[(X-g(Y))^2]=\mathbb E[(X-M)^2]+\mathbb E[(M-g(Y))^2].$$

The second term is nonnegative and becomes zero when $g(Y)=M$. Conditional expectation therefore minimizes mean squared error among all predictions using only $Y$.

In the die example, $\mathbb E[X]=3.5$. With no information, the best constant prediction has error $\operatorname{Var}(X)=35/12$. Knowing parity reduces the error to

$$\mathbb E[(X-M)^2]=\frac{4+4+0+0+4+4}{6}=\frac83.$$

The reduction is $35/12-8/3=1/4$. You can distinguish more outcomes, so your prediction can lie in a larger subspace:

$$\underbrace{\{c\mathbf 1:c\in\mathbb R\}}_{\text{no information}}\subset\underbrace{S_Y}_{\text{parity known}}\subset\underbrace{\mathbb R^6}_{\text{exact roll known}}.$$

Projection onto the last space returns $X$ itself, with zero error.

### Scope and a check

Conditional expectation projects onto all functions of $Y$. A best linear prediction $a+bY$ projects onto $\operatorname{span}\{\mathbf 1,Y\}$. These spaces coincide for the binary $Y$ above; they generally differ when $Y$ has more values.

The same projection interpretation holds beyond finite spaces when $\mathbb E[X^2]<\infty$, using square-integrable random variables. Conditional expectation also exists for integrable $X$ without a finite second moment, but the squared-distance argument then need not apply. Outcomes of probability zero do not affect the geometry; predictions are identified when they agree with probability one.

To check the connection, let $Y$ tell you whether the die roll is at most $2$.

1. Write the pattern of vectors in $S_Y$ using two unknown values $a,b$.
2. Average $X$ within each group to find $M=\mathbb E[X\mid Y]$.
3. Check that $X-M$ is perpendicular to an arbitrary vector in $S_Y$ under $\langle\cdot,\cdot\rangle_P$.
