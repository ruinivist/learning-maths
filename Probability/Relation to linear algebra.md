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

TODO: more comparisons.
