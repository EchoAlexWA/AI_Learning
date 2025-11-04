# Gradient Method
## Overview
The Gradient Method, also known as Gradient Descent, is an optimization algorithm used to minimize a function by iteratively moving towards the steepest descent, which is determined by the gradient. It is widely used in machine learning and deep learning for training models by minimizing loss functions.

Mathematically, given a differentiable function \( f: \mathbb{R}^n \to \mathbb{R} \), the gradient method updates the parameters \( \theta \) using the following rule:
$$
\theta_{k+1} = \theta_k - \alpha \nabla_\theta f(\theta_k),
$$
where:
- \( \theta_k \) is the current parameter vector,
- \( \alpha \) is the learning rate (a small positive scalar),
- \( \nabla_\theta f(\theta_k) \) is the gradient of the function at \( \theta_k \).

The process is repeated until convergence, which can be determined by a stopping criterion such as a maximum number of iterations or when the change in the function value is below a certain threshold.

## Batched vs. Stochastic Gradient Descent
There are two main variants of the gradient method: Batched Gradient Descent and Stochastic Gradient Descent (SGD).

### Batched Gradient Descent
In Batched Gradient Descent, the gradient is computed using the entire dataset.
$$
\theta_{k+1} = \theta_k - \alpha  \frac{1}{N} \sum_{i=1}^{N} \nabla_\theta f(\theta_k; x_i, y_i),
$$
where:
- \( N \) is the total number of samples in the dataset,
- \( (x_i, y_i) \) are the individual data points.

### Stochastic Gradient Descent (SGD)
In Stochastic Gradient Descent, the gradient is computed using only a single data point (or a small batch) at each iteration.
$$
\theta_{k+1} = \theta_k - \alpha \nabla_\theta f(\theta_k; x_i, y_i),
$$
where:
- \( (x_i, y_i) \) is a randomly selected data point from the dataset.

For each round of updates, SGD typically goes through all data points in a random order or just increases the index cyclically.

