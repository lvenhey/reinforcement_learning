## RL Lesson 6: Stochastic Approximation

SA refers to broad class of stochastic iterative algorithms solving root finding or optimization problems with no need to know the expression of the objective function nor its derivative(导数).

### 1、Mean Estimation

Q: How do we calculate the mean value of expectation?

A: We use the incremental and iterative manner to calculates the average value.

$$
w_{k+1} = w_k - \frac{1}{k}(w_k-x_k)
$$

**k** represents discrete-time series.

Attention that the mean estimate is not accurate in the beginning due to insufficient samples.

_____

### 2、Robbins-Monro algorithm

#### Before the algorithm

Suppose $J(w)$  is  an objective function to be minimized. Then the optimization problem  can be converged to:

$$
g(w) = \nabla_w J(w) = 0
$$

It becomes a sufficient condition when $J(w)$ only has one extremum(极点).

#### PS What is the $\nabla$ ?

It's a vector showing the changing rate of one function.

$$
(\frac{\partial f}{\partial x},\frac{\partial f}{\partial y})
$$

____

#### Robbins-Monro algorithm

The algorithm to solve this kind problem $g(w) = \nabla_w J(w) = 0$ .

And the **algorithm** is  more abstractly like,

$$
\omega_{k+1} = \omega_k -\alpha_k \tilde{g}(\omega_k,\eta_k), \quad k=1,2,3,....
$$

where

* $\omega_k$ is the kth estimate of the root(根)
* $\tilde{g}(\omega_k,\eta_k) = g(\omega_k) + \eta_k$ is the kth noisy observation
* $\alpha_k$ is a positive coefficient.

After sufficient many times iteration, the $\omega$ eventually converges to the $\omega^{ *}$, which should be the root to the equation $g(w) = \nabla_w J(w) = 0$ .

____

#### Rigorous convergence result

* $0<c_1 \le \nabla_\omega g(\omega) \le c_2 $ 

  ensures the root of $g(\omega)$ exist

* $\sum_{k=1}^{\infty} a_k^2 < \infty$ and  $\sum_{k=1}^{\infty} a_k = \infty$ 

​	The first one ensures the sequences {$\omega$ } converges.

​	The second one prevents that initial guess $\omega_1$ can be chosen arbitrarily far away from the root $\omega^{ *}$ .

* $E[\eta_k | H_k]= 0$ and $E[\eta_k^2 | H_k] < \infty$ where $H_k = {{} \omega_k ,\omega_{k-1} {}}$ 

_____

#### Application to mean estimation

Recall that,

$$
\omega_{k+1} = \omega_k + \alpha_k (x_k - \omega_k)
$$

How to prove $\omega_k$ converges to $E[X]$ with $\alpha_k$ unknown?

1. Let 

$$
g(\omega) \doteq \omega - E[X]
$$

​	and we know that E[X] is  constant.

2. The observation is

$$
\tilde{g}(\omega,x) \doteq \omega -x \\
=(\omega - E[X])+(E[X]-x) \\
\doteq g(\omega)+\eta
$$

3. Using the RM algorithm for solving $g(\omega) = 0$

$$
\omega_{k+1} = \omega_k -\alpha_k \tilde{g}(\omega_k,\eta_k), \quad k=1,2,3,....
$$

 	which can be rewritten like,
$$
\omega_{k+1} = \omega_k -\alpha_k (\omega_k -x_k)
$$
​	which is exactly the mean estimation algorithm!!!!

++++

### 3、 Stochastic gradient descent

#### Problem statement

We aim to solve the following optimization problem:

$$
\min_{\omega} J(\omega) = E[f(\omega,X)]
$$

* w is the parameter to be optimized
* X is a random variable and we do not know its contribution
* w and X can be either scalars(标量) or vectors

____

#### GD、BGD、SGD

* GD(gradient descent)

Before SGD, GD should firstly be introduced:

$$
\omega_{k+1} = \omega_k - \alpha_k \nabla_{\omega}E[f(\omega_k,X)]\\=\omega_k - \alpha_k E[\nabla_{\omega} f(\omega_k,X)]
$$
whose drawback is that the expected value is difficult to obtain!

* BGD(batch gradient descent)

$$
E[\nabla_{\omega} f(\omega_k,X)] \approx \frac{1}{n} \sum_{i=1}^n \nabla_\omega f(\omega_k,X)
$$

* SGD

$$
\omega_{k+1} = \omega_k - \alpha_k \nabla_{\omega}f(\omega_k,x_k)
$$

Replace the true gradient $E[\nabla_{\omega} f(\omega_k,X)] $ by the stochastic gradient $\nabla_{\omega}f(\omega_k,x_k)$ 

But is SGD truly useful? And is it efficient?
