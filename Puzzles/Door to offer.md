# Door to offer

There are two guards: one always tells the truth, and the other always lies. You need to choose the right door. What do you do?

## Solution

Let:

- $D=1$: This guard's door leads to the offer.
- $L=1$: This guard lies.
- $Q$: Truth value of our question.
- $Y$: Guard's actual answer.

Since lying flips an answer:

$$Y=Q\oplus L$$

### 1. Deriving our question

We want $Y=D$, so:

$$Q\oplus L=D$$

$$\boxed{Q=D\oplus L}$$

XOR means exactly one statement is true.

Therefore, ask:

"Is exactly one of these true: your door leads to the offer, or you are a liar?"

Then:

$$Y=(D\oplus L)\oplus L=\boxed D$$

- Yes → This door.
- No → Other door.

### 2. Deriving the common answer

The common question is:

"Would the other guard say your door leads to the offer?"

We can derive it by instead requiring $Y=\neg D$.

$$Q\oplus L=\neg D$$

$$Q=\neg D\oplus L$$

Using XOR properties:

$$\boxed{Q=D\oplus\neg L}$$

Here:

- $D$ represents the truth about this door.
- $\neg L$ represents whether the other guard lies.

Thus, $D\oplus\neg L$ models what the other guard would answer about this door.

So we ask what that guard would say.

The actual response is:

$$Y=(D\oplus\neg L)\oplus L$$

$$\boxed{Y=\neg D}$$

- Yes → Other door.
- No → This door.

Key insight: Both questions come from the same Boolean model. We simply choose whether we want the answer to equal $D$ or $\neg D$, then work backwards to formulate the question.
