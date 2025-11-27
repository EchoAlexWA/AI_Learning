Entropy is a fundamental concept in information theory that quantifies the uncertainty or unpredictability of a random variable or a set of possible outcomes. It is often used to measure the amount of information contained in a message or the efficiency of a coding scheme. It is also used in machine learning, particularly in decision tree algorithms, to determine the best feature to split the data.

**Shannon Entropy**, named after Claude Shannon, is defined mathematically as:
$$
H(x)=-\sum_{i=1}^k p_i \log_2(p_i)
$$
where:
- X: A discrete random variable with possible outcomes ${x_1, x_2, ..., x_k}$
- $p_i$: The probability of outcome $x_i$.

**Conditional Entropy**
Conditional entropy measures the amount of uncertainty remaining about a random variable Y given that the value of another random variable X is known. It is defined as:
$$
H(Y|X) = -\sum_{x \in X} p(x) H(Y|X=x)
$$
where:
- Y: A discrete random variable whose uncertainty we want to measure.
- X: A discrete random variable that we condition on.
- $p(x)$: The probability of the outcome x of the random variable X.

**Information Gain**
Information Gain (IG) is a measure used to quantify the reduction in uncertainty about a random variable Y after observing another random variable X. It is defined as the difference between the entropy of Y and the conditional entropy of Y given X:
$$
Gain(Y, X) = H(Y) - H(Y|X)
$$

**Cross-Entropy**
Cross-entropy is a measure of the difference between two probability distributions. It is commonly used in machine learning for classification tasks. The cross-entropy between a true distribution p and an estimated distribution q is defined as:
$$
H(p, q) = -\sum_{i} p_i \log_2(q_i)
$$
where:
- p: The true probability distribution.
- q: The estimated probability distribution.
- i: The possible outcomes.
Cross-entropy loss function is often used in training classification models, where the goal is to minimize the difference between the predicted probabilities and the true labels. When there are 2 classes, it is defined as:$$
L = -\frac{1}{N} \sum_{i=1}^{N} [y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)]
$$

When there are multiple classes, it is defined as:$$
L = -\frac{1}{N} \sum_{i=1}^{N} \sum_{c=1}^{C} y_{i,c} \log(\hat{y}_{i,c})
$$
where:
- N: The number of samples.
- C: The number of classes.
Usually, $y_{i,c}=1$ for the correct class and 0 for the others. Under one-hot encoding, cross-entropy is equivalent to negative log likelihood.

**Kullback-Leibler Divergence**
Kullback-Leibler (KL) divergence is a measure of how one probability distribution diverges from a second, expected probability distribution. It is defined as:
$$
D_{KL}(P || Q) = \sum_{i} p_i \log_2\left(\frac{p_i}{q_i}\right)
$$
where:
- $p_i$: The true probability distribution.
- $q_i$: The estimated probability distribution.
- i: The possible outcomes.
  When one-hot encoding is used, KL divergence is equivalent to cross-entropy of P and Q.

  **Jensen-Shannon Divergence**
Jensen-Shannon (JS) divergence is a symmetric and finite measure of similarity between two probability distributions. It is defined as:
$$
D_{JS}(P || Q) = \frac{1}{2} D_{KL}(P || M) + \frac{1}{2} D_{KL}(Q || M)
$$
where:
- P and Q: The two probability distributions being compared.
- M: The average of the two distributions, defined as $M = \frac{1}{2}(P + Q)$.
- $D_{KL}$: The Kullback-Leibler divergence.