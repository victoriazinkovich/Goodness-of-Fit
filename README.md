# Goodness-of-Fit
In this work we have tried to realise and reproduce the results of the article "A Kernel Test of Goodness of Fit" by K. Chwialkowski, et al.  The main idea of this article is to derive a statistical test, which would help to determine for given sample set whether its distribution matches some reference/target distribution. 

## Problem Statement

The main idea of this article is to **derive a statistical test**, both for i.i.d. and non-i.i.d. samples, which would help to determine for given a set of samples $\{Z_i\}^n_{i=1}$ with distribution $Z_i \sim q$, **whether q matches some reference or target distribution p**. Actually, this problem was already partially solved by Gorham & Mackey (2015), but their approach is problematic to apply since it has the following drawbacks:

<br>

1. The function class used is really **complicated**, so to obtain a sample quality measure, one should solve a non-trivial linear program

2. Due to the complexity of the function class used, it is **not clear** how one would **compute p-values** for this statistic


So since the problems above exists, it was necessary to make a new test, which is the subject of this article.

<br>


## Methods

*In this chapter, we will not show where every formula in the paper came from, but we will give what we thought were the most important results for understanding what is going on in the paper.*

<br>

The key idea of this article is to define a statistical
test of goodness-of-fit, based on a Stein discrepancy computed in a **Reproducing Kernel Hilbert Space (RKHS)**. In this space many intresting useful results appear, which makes our life better (in terms of computing statistical tests)! Specifically, our goal is to write the **maximum discrepancy** between target distribution $p$ and observed sample distribution $q$ in a RKHS.

Let's denote by $\mathcal{F}$ $-$ the RKHS of functions on $\mathbb{R}^d$ with reproducing kernel $k$, and by $\mathcal{F}^d$ $-$ the product RKHS consisting of elements $f:=\left(f_1, \ldots, f_d\right)$ with the standard inner product:

<br>

 $$
 \langle f, g\rangle_{\mathcal{F}^d}= \sum_{i=1}^d\left\langle f_i, g_i\right\rangle_{\mathcal{F}}
 $$

<br>

Also, we will define a Stein operator $T$ acting on $f \in \mathcal{F}^d$:

<br>

  $$
  T_p f:=\sum_{i=1}^d\left(\frac{\partial \log p(x)}{\partial x_i} f_i(x)+\frac{\partial f_i(x)}{\partial x_i}\right)
  $$

<br>

Suppose a random variable $Z \sim q$ and $X \sim p$. It can be shown, that the Stein operator can be expressed by defining a function that depends on gradients of the logdensity and the kernel:

<br>

$$
\mathbb{E} T_p f(Z)=\left\langle f, \mathbb{E} \xi_p(Z)\right\rangle_{\mathcal{F}^d}=\sum_{i=1}^d\left\langle f_i, \mathbb{E} \xi_{p, i}(Z)\right\rangle_{\mathcal{F}}
$$

where,

$$
\xi_p(x, \cdot):=[\nabla \log p(x) k(x, \cdot)+\nabla k(x, \cdot)]
$$

<br>

Also, using integration by parts it can be seen for $X$ from the target measure that $\mathbb{E}\left(T_p f\right)(X)=0$ which allows to express Stein discrepancy as:

<br>

$$
\begin{equation}
S_p(Z) & :=\sup _{\|f\|<1} \mathbb{E}\left(T_p f\right)(Z)-\mathbb{E}\left(T_p f\right)(X) \\
& =\sup _{\|f\|<1} \mathbb{E}\left(T_p f\right)(Z) \\
& =\sup _{\|f\|<1}\left\langle f, \mathbb{E} \xi_p(Z)\right\rangle_{\mathcal{F}^d} \\
& =\left\|\mathbb{E} \xi_p(Z)\right\|_{\mathcal{F}^d},
\end{equation}
$$

$$
\begin{aligned}
S_p(Z) & :=\sup _{\|f\|<1} \mathbb{E}\left(T_p f\right)(Z)-\mathbb{E}\left(T_p f\right)(X) \\
& +\nabla \log p(y)^{\top} \nabla_x k(x, y) \\
& +\nabla \log p(x)^{\top} \nabla_y k(x, y) \\
& +\left\langle\nabla_x k(x, \cdot), \nabla_y k(\cdot, y)\right\rangle_{\mathcal{F}^d}
\end{aligned}
$$

<br>

Finally, to obtain a key result of the article, we need two theorems that we will cite here without proof:

<br>

**Theorem 1.**
If $E h_p(Z, Z)<\infty$, then $S_p(Z)^2=$ $\left\|\mathbb{E} \xi_p(Z)\right\|_{\mathcal{F}^d}=\mathbb{E} h_p\left(Z, Z^{\prime}\right)$

<br>

**Theorem 2.**
Let $q, p$ be probability measures and $Z \sim q$. if some conditions concerning finiteness of the expectation matrix are fulfilled, then $S_p(Z)=0$ if and only if $p=q$.

<br>

These expressions also introduce the function $h_p(Z, Z^{\prime})$, which can be represented as the sum of several summands depending on the kernel density function and its derivatives:

<br>

$$
\begin{aligned}
h_p(x, y):= & \nabla \log p(x)^{\top} \nabla \log p(y) k(x, y) \\
& +\nabla \log p(y)^{\top} \nabla_x k(x, y) \\
& +\nabla \log p(x)^{\top} \nabla_y k(x, y) \\
& +\left\langle\nabla_x k(x, \cdot), \nabla_y k(\cdot, y)\right\rangle_{\mathcal{F}^d}
\end{aligned}
$$

<br>

**Finally**, it follows from these two theorems that the Stein discrepancy can serve as an indicator of the similarity of the distributions of $p$ and $q$! And now our task is to find out when $S_p(Z) = 0$ according to Theorem 2.

<br>

$$
\boxed{
\text{when holds} \quad S_p(Z)= \mathbb{E} h_p\left(Z, Z^{\prime}\right) = 0  \quad \text{?}
}
$$

<br>

This will be discussed in more detail in the chapter below on Experiment 1.
