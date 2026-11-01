# Binomial Distribution

## Problem 1: Customer conversions

A company independently contacts potential customers. Each customer has a $50\%$ probability of becoming a paying customer. The company contacts $6$ customers. Let $X$ be the number of conversions.

1. Find $P(X=4)$, $P(X\geq 3)$, and $P(2\leq X\leq 5)$. Find the mean and variance of $X$.
2. Given that at least $3$ customers converted, find the probability that exactly $4$ converted.
3. Find the minimum number of customers the company must contact to have at least a $95\%$ probability of getting one or more conversions. Derive the result for a general probability $p$ first.
4. The first $3$ customers did not convert. Assuming conversions remain independent with the same probability, does this change the probability that at least one of the next $3$ customers converts? Explain.

## Problem 2: Majority voting

A team builds $5$ binary classifiers. Each classifier independently predicts the correct label with probability $2/3$. The ensemble uses majority voting, so at least $3$ classifiers must be correct for the ensemble to be correct.

1. Find the probability that the ensemble predicts correctly. Compare it with the accuracy of one classifier.
2. Given that the ensemble predicted correctly, find the probability that exactly $4$ classifiers were correct.
3. Suppose one classifier has accuracy $3/4$ and the other four each have accuracy $1/2$. Assume the classifiers' correctness events are independent. Find the probability that the ensemble predicts correctly. Does the number of correct predictions still have a binomial distribution?
4. Suppose the classifiers' errors are strongly positively correlated. Can you still use the original binomial calculation? Explain whether majority voting must improve accuracy in this situation.

### Follow-up: Majority voting vs. asymmetric decision rules

Return to the original $5$ classifiers. Suppose the ensemble predicts label $1$ only when **at least $4$ classifiers vote for label $1$**. Otherwise, it predicts label $0$.

Let $Y\in\{0,1\}$ denote the true label. Assume that, conditional on either true label, each classifier independently predicts the correct label with probability $2/3$. Let $P(Y=1)=\alpha$.

5. Answer the following:
   - Find $P(\text{ensemble correct}\mid Y=1)$.
   - Find $P(\text{ensemble correct}\mid Y=0)$.
   - Express the overall probability of a correct prediction in terms of $\alpha$.
   - Explain why the class prevalence $\alpha$ matters under this decision rule but was unnecessary under the original majority-voting rule.
   - Generalize: Under what conditions can we calculate the accuracy of a voting ensemble without knowing the distribution of the true labels?
   - Remember this: The ensemble needs 4 correct votes if $Y=1$, but only 2 if $Y=0$, so we need the class prevalence $P(Y=1)=\alpha$

## Problem 3: Testing a success-rate claim

A company claims its software completes a task successfully $80\%$ of the time. You independently test it on $100$ tasks and observe $72$ successes. Assume the outcomes are independent and identically distributed.

1. Under the company's claim, express the exact probability of observing $72$ or fewer successes as a binomial sum. You do not need to evaluate the sum numerically.
2. Approximate this probability using a normal distribution. Is a continuity correction needed? Explain.
3. Formulate a hypothesis test for whether the true success probability is less than $80\%$. At the $5\%$ significance level, would you reject the null hypothesis?
4. Find the largest number of successes $k$ such that observing $k$ or fewer successes would lead you to reject the null hypothesis at the $5\%$ level. State the exact criterion before approximating it. You may use $z_{0.05}\approx -1.645$.
5. If the success probability is unknown, find the estimate of $p$ that maximizes the likelihood of observing $72$ successes out of $100$ trials. Derive your answer.

## Problem 4: Identifying the production line

A factory has two production lines:

- Line A produces defective items with probability $0.01$.
- Line B produces defective items with probability $0.03$.

One line is selected with equal probability and produces $100$ independently manufactured items. You inspect all the items and find exactly $2$ defectives.

1. Find the probability of observing exactly $2$ defective items under each production line. Leave your answers as exact expressions.
2. Using Bayes' theorem, find the probability that Line B was selected, given that you observed exactly $2$ defectives. Simplify your expression without evaluating large powers.
3. Approximate both likelihoods using a Poisson distribution. Explain why the approximation is reasonable and compare the resulting posterior probability with the exact expression.
4. Now suppose a warehouse contains exactly $60$ defective items among $10{,}000$ items. You randomly sample $100$ items without replacement. Is the number of defectives in the sample binomial? If not, name the correct distribution and explain when a binomial approximation might be reasonable.
