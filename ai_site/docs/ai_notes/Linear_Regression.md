## Ordinary Linear Regression
Consider the data set $D=\{(x_1, y_1), (x_2, y_2), \ldots, (x_n, y_n)\}$.

Firstly, we consider the case when y is a scalar (i.e., univariate linear regression).

Assume $x\in \mathbb{R}^d, y\in \mathbb{R}$ and $X=\begin{bmatrix}x_1^T \\ x_2^T \\ \vdots \\ x_n^T\end{bmatrix} \in \mathbb{R}^{n\times d}$.

The goal of linear regression is to find $w\in \mathbb{R}^d$ and $b\in \mathbb{R}$ such that the predicted values $\hat{y} = w^T x + b$ are as close as possible to the true values $y$.

We need a loss function to measure the difference between the predicted values and the true values. A common choice is the mean squared error (MSE):
$$L(w, b) = \frac{1}{n} \sum_{i=1}^{n} \frac{1}{2}(y_i - (w^T x_i + b))^2.$$

The objective is to find the parameters $w$ and $b$ that minimize the loss function:
$$w, b = \arg\min_{w, b} L(w, b).$$

$$
\begin{aligned}
\nabla_w L(w, b) &= -\frac{1}{n} \sum_{i=1}^{n} (y_i - (w^T x_i + b)) x_i, \\
\nabla_b L(w, b) &= -\frac{1}{n} \sum_{i=1}^{n} (y_i - (w^T x_i + b)), \\
\nabla_w^2 L(w, b) &= \frac{1}{n} \sum_{i=1}^{n} x_i x_i^T, \\
\nabla_{wb}^2 L(w, b) &= \frac{1}{n} \sum_{i=1}^{n} x_i, \\
\nabla_b^2 L(w, b) &= 1.
\end{aligned}
$$

We define 
$$
\begin{aligned}
H &= \begin{bmatrix}\nabla_w^2 L(w, b) & \nabla_{wb}^2 L(w, b) \\ (\nabla_{bw}^2 L(w, b))^T & \nabla_b^2 L(w, b)\end{bmatrix}\\
&= \begin{bmatrix}\frac{1}{n} \sum_{i=1}^{n} x_i x_i^T & \frac{1}{n} \sum_{i=1}^{n} x_i \\ \frac{1}{n} \sum_{i=1}^{n} x_i^T & 1\end{bmatrix} \\
&=\frac{1}{n} \sum_{i=1}^{n} \begin{bmatrix}x_i \\ 1\end{bmatrix} \begin{bmatrix}x_i^T & 1\end{bmatrix}\\
&=\frac{1}{n} \sum_{i=1}^{n} \tilde{x}_i \tilde{x}_i^T, & (\tilde{x}_i = \begin{bmatrix}x_i \\ 1\end{bmatrix})
\end{aligned}
$$
as the Hessian matrix of $L(w, b)$. 

From the discussion above, we can see that $H$ is positive semidefinite since for any vector $v\in \mathbb{R}^{d+1}$,
$$
v^T H v = \frac{1}{n} \sum_{i=1}^{n} \left\langle v, \tilde{x}_i \right\rangle^2 \geq 0.
$$
When $\tilde{x}_1,\cdots,\tilde{x}_n$ can span $\mathbb{R}^{d+1}$, $H$ is positive definite. Thus, $n$ is at least $d+1$ for $H$ to be positive definite.

When $H$ is positive definite, $L(w, b)$ is a strictly convex function, and there exists a unique global minimizer $(w^*, b^*)$. We can find the optimal solution by setting the gradients to zero:
$$
\begin{aligned}
\nabla_w L(w, b) &= 0\Leftrightarrow \frac{1}{n} \sum_{i=1}^{n} (w^T x_i + b - y_i)x_i = 0, \\
&\Leftrightarrow X^T (Xw + b\mathbf1 - Y) = 0, \\
\nabla_b L(w, b) &= 0\Leftrightarrow \frac{1}{n} \sum_{i=1}^{n} (w^T x_i + b - y_i) = 0,\\
&\Leftrightarrow \mathbf1^T (Xw + b\mathbf1 - Y) = 0,
\end{aligned}
$$

When X has full column rank, we can solve the above linear system to get the unique solution $(w^*, b^*)$:
$$
\begin{aligned}
w^*&=(X^TX)^{-1} X^T (Y - b\mathbf 1),\\
b^* &= \bar{y} - (w^*)^T \bar{x}, \\
\end{aligned}
$$


We can also express the solution in a closed form by augmenting the data matrix $X$ with a column of ones to account for the bias term $b$:
$$
\tilde{X} = \begin{bmatrix}X & \mathbf{1}\end{bmatrix} \in \mathbb{R}^{n\times (d+1)}.
$$

Mninimizing the loss function is equivalent to solving the normal equations:
$$
\begin{aligned}
L(\tilde{w})=\frac 12 \left\| \tilde{X} \tilde{w} - Y \right\|_2^2\\
\nabla_{\tilde{w}} L(\tilde{w}) = \tilde{X}^T (\tilde{X} \tilde{w}-Y) = 0\\
\Leftrightarrow \tilde{X}^T \tilde{X} \tilde{w} = \tilde{X}^T Y\\
\end{aligned}
$$

When $\tilde{X}$ has full column rank, the unique solution is given by:
$$
\tilde{w}^* = (\tilde{X}^T \tilde{X})^{-1} \tilde{X}^T Y.
$$

## error aspect
We could also analyze the linear regression from the error aspect. Assume the true model is
$$y = w_{true}^T \tilde{x} + \epsilon,$$
where $\epsilon$ is the noise term with zero mean and variance $\sigma^2$.
We can obtain the MLE (Maximum Likelihood Estimation) of $w$ and $b$. Under the assumption that the noise term $\epsilon$ follows a normal distribution, i.e., $\epsilon \sim \mathcal{N}(0, \sigma^2)$, the likelihood function of the observed data is given by:
$$
P(Y|X, w, b) = \prod_{i=1}^{n} \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(y_i - w^T \tilde{x_i})^2}{2\sigma^2}\right).
$$
Maximizing the likelihood function is equivalent to minimizing the negative log-likelihood, which leads to the same objective as minimizing the mean squared error (MSE):
$$
\begin{aligned}
L(w) &:= -\log P(Y|X, w, b) \\
&= \frac{1}{2\sigma^2} \sum_{i=1}^{n} (y_i - w^T \tilde{x_i})^2 + \frac{n}{2} \log(2\pi\sigma^2)\\
&\propto \sum_{i=1}^{n} (y_i - w^T \tilde{x_i})^2.
\end{aligned}
$$

This shows that the ordinary linear regression can be interpreted as finding the MLE of the parameters under the assumption of normally distributed errors, which justifies the use of the mean squared error as the loss function.

 Note that the value of $𝜎^2$ does not affect the choice of $w$ and $b$.


## Assumptions of Linear Regression
1. **Linearity**: The relationship between *x* and the mean of *y* is linear.  

2. **Homoscedasticity**: The variance of residual is the same for any value of *x*.  

3. **Independence**: Observations are independent of each other.  

4. **Normality of residuals**: For any fixed value of *x*, *y* is normally distributed, or we can say the residuals (errors) should follow a **normal distribution**.

## Covariance Aspects
For $x\in \mathbb{R}^d$ which is a random variable vector, we have
$$
\begin{aligned}
\mathrm{Cov}(y, x) &= \mathrm{Cov}(w^T x + b, x) \\
&= \mathrm{Cov}(w^T x, x) + \mathrm{Cov}(b, x) \\
&= \mathrm{Cov}(w^T x, x) + 0 \\
&= w^T \mathrm{Var}(x) \\
\Rightarrow w &= \mathrm{Var}(x)^{-1}\mathrm{Cov}(x, y) \\
\end{aligned}
$$

We can use unbiased sample covariance and variance to estimate $w$:
$$
\begin{aligned}
\hat{w} &= \hat{\mathrm{Var}}(x)^{-1}\hat{\mathrm{Cov}}(x, y) \\
&= \left(\frac{1}{n-1} \sum_{i=1
}^{n} (x_i - \bar{x})(x_i - \bar{x})^T\right)^{-1} \left(\frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})\right) \\
&= \left(\sum_{i=1}^{n} (x_i - \bar{x})(x_i - \bar{x})^T\right)^{-1} \left(\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})\right) \\
&= (X^T X - n \bar{x} \bar{x}^T)^{-1} (X^T Y - n \bar{x} \bar{y}) \\
\end{aligned}
$$