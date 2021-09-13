---
layout: distill
title: Stochastic Integral
date: 2021-09-06
description: Note collection of Stochastic Integral
---

### Introduction

This note is to summarize the stochastic integral of <a href="https://almostsuremath.com/stochastic-calculus/">AlmostSure's blog</a>.

By the Riemann-Stieltjes integral $$\int g df$$ is well-defined if $$g$$ is continuous and $$f$$ is **differentiable**. However, stochastic processes do not always satisfy the differentiation condition, for example, Brownian motion which is nowhere differentiable. Therefore, we need new way to define integral involving stochastic process.

The stochastic integration proposed by Kiyoshi Ito defines integrals for stochastic process including adapted processes then extending to martingales and semimartingales. The integral is in fact defined via Lebesgue  sense (or <a href="https://en.wikipedia.org/wiki/Dominated_convergence_theorem">dominated convergence theorem</a>), i.e,

$$
\lim_{n \to \infty} \int \lvert f_n - f\rvert d\mu = 0 \quad \Rightarrow \quad \lim_{n \to \infty} \int f_n d\mu = \int f d\mu
$$

Idea: to define the integrand of simple elementary process which statisfied the dominated convergence theorem.

With an elementary predictable process $\xi$ defined as 

$$
\xi_t = Z_0 1_{\{t=0\}} + \sum_{k=1}^n Z_k 1_{\{s_k < t\leq t_k\}}
$$

then 

$$
    \int_0^t \xi dX = \sum_{k=1}^n Z_k (X_{t_k \wedge t} - X_{s_{k} \wedge t})
$$

If $$\xi^n \to \xi$$ and bounded, then $$\int_0^t\xi^n dX \to \int_0^t \xi dX$$ 

### Quadratic Variations and Integration by Parts

+ Increment $$\delta X_t = X_{t + \delta t} - X_t$$
+ Consider product $$\delta (XY) = X\delta Y + Y\delta X + \delta X \delta Y$$
+ Chop $$[0, t]$$ into $$n$$ parts and sum all terms

$$
    X_t Y_t - X_0Y_0 = \sum_{k=1}^n X_{t_k}\delta Y_{t_k} + \sum_{k=1}^n Y_{t_k}\delta X_{t_k} + \sum_{k=1}^n \delta X_{t_k} \delta Y_{t_k}
$$

Observation:
+ If these processes are **continuously differentiable**, $$\delta X_{t_k} \delta Y_{t_k} = \mathcal{O}(1/n^2)$$, while the first two first terms are $$\mathcal{O}(1/n)$$.

$$
X_t Y_t - X_0Y_0 = \sum_{k=1}^n \underbrace{X_{t_k}\delta Y_{t_k}}_{\mathcal{O}(1/n)} + \sum_{k=1}^n \underbrace{Y_{t_k}\delta X_{t_k}}_{\mathcal{O}(1/n)} + \sum_{k=1}^n \underbrace{\delta X_{t_k} \delta Y_{t_k}}_{\mathcal{O}(1/n^2) \to 0} = \int_0^t X dY + \int_0^t Y dX.
$$

+ On the other hand, if $$X, Y$$ are Brownian motions, as we know, $$\delta X = \mathcal{O}(\sqrt{\delta t})$$. So the last term does not vanish, is the reason for introducing *quadratic covariation* of $$X$$ and $$Y$$.

Define:
+ $$[X]_t^P = \sum_{n=1}^\infty (X_{\tau_n \wedge t} - X_{\tau_{n-1} \wedge t})^2$$

+ $$[X, Y]_t^P = \sum_{n=1}^\infty (X_{\tau_n \wedge t} - X_{\tau_{n-1} \wedge t})(Y_{\tau_n \wedge t} - Y_{\tau_{n-1} \wedge t})$$

**Theorem (Quadratic Variations and Covariations)**
Let $$X, Y$$ be semimartingales. Then, there exist cadlag adapted process $$[X]$$ and $$[X, Y]$$. For any sequence $$P_n$$ of stochastic partition on $$\mathbb{R}_+$$, 
+ $$[X]^{P_n} \to [X]$$
+ $$[X, Y]^{P_n} \to [X, Y]$$

These convergences are of <a href="https://almostsuremath.com/2009/12/22/u-c-p-convergence/">uniform convergence on compacts in probability</a>(ucp)

**Theorem (Integration by Parts)** If $$X, Y$$ are semimartingales then

$$
    XY = X_0Y_0 \int X_{-} dY + \int Y_{-}dX + [X,Y]
$$

**Quadratic variation of Brownian motion** 
Because Brownian motion, $$B$$, is a semimartingale, there exists quadratic varitions. Let us partition and define

$$
    V^n = \sum_{k=1}^n (B_{kt/n} - B_{(k-1)t/n})^2
$$

By defintion of Brownian motion, $$B_{kt/n} - B_{(k-1)t/n} \sim \mathcal{N}(0, t/n)$$.

Squares of these differences have mean $$t/n$$ and variance $$2t^2/n^2$$ (in fact, it is somewhat similar to chi-squared distribution).

$$
    \mathbb{E}[V^n] = t \quad, \quad \text{Var}(V^n) = 2t^2/n \to 0 \quad \text{ when } n \to \infty
$$

So we can say when $$n \to \infty$$

$$
    \mathbb{E}[(V^n - t)^2] \to 0 \quad \Rightarrow [B]_t = t
$$

For covariations of two Brownian motions $$B^1, B^2$$, the following resembles the above result

$$
    [B^1, B^2]_t = \rho t
$$

where $$\rho$$ is the correlation between $$B^1$$ and $$B^2$$

### Properties of Quadratic Variations
Importance: Lead to Ito's lemma

Recall the notation $$\Delta [X]_t = [X]_t - [X]_{t-}$$ is the jump of a process.

**Lemma** If $$X, Y$$ are semimartingales then

$$
\Delta [X,Y] = \Delta X \Delta Y
$$

### Ito's Lemma

We do calculus with a function $$f(x)$$ where $$x(t)$$ is a stochastic process. Traditional calculus cannot apply here because we often do have $$x(t)$$ differentiable. 


Ito's lemma works on semimartingales (cadlag, adapted, exist integral), and can be expressed as

$$
df(X) = f'(X)dX + \frac{1}{2}f''(X)dX^2
$$

This can be derive from a Taylor expansion. Here, $$dX^2 = d[X]$$ (quadratic variation). 

**Theorem (Ito's Lemma)** Let $$X=(X^1, \dots, X^d)$$ be continous d-dimensional semimartingale. For any twice differential function $$f$$, $$f(X)$$ is a semimartingale and

$$
df(X) = \sum D_if(X)dX^i + \frac{1}{2} \sum D_{ij}f(X)d[X^i, X^j]
$$

Or in the integration form,

$$
f(X) = f(X_0) + \sum_{i=1}^d \int D_if(X)dX^i + \frac{1}{2} \sum_{i,j=1}^d \int D_{ij}f(X)d[X^i, X^j]
$$

Key obsevarion for the proof is the properties of covariations

$$
[f(X), Y] = \sum_{i=1}^d \int D_i f(X)d[X^i, Y]
$$

**Proof** 
Let $$\delta X = X_t - X_s$$, and from Taylor expansion

$$
    f(X_t) = f(X_s) + D_if(X_s)\delta X^i + \frac{1}{2} D_{ij}f(X_s)\delta X^i \delta X^j + R_{st}
$$

We can say that $$R_{st}$$ vanishes faster than other term. We perform partition just like the variation and covariation, 

$$
    f(X_T) = F(X_0) + \sum_k D_if(X_{t^n_{k-1}})\delta_{n,k} X^i + \frac{1}{2} \sum_k D_{ij}f(X_{t^n_{k-1}})\delta_{n,k} X^i \delta_{n,k} X^j + R_{t^n_{k-1},t^n_{k}}
$$

Next, the proof is based on two results

$$
\sum_{k=1}^n U_{t^n_{k-1}}\delta_{n, k}Y \to \int_0^T U_{-} dY \quad, \quad \sum_{k=1}^n U_{t^n_{k-1}}\delta_{n, k}Y\delta_{n, k}Z \to \int_0^T U_{-} d[Y, Z]
$$

Replace $$U$$ with respective terms, to obtain the finally result.

### The generalized Ito Formula

Motivation: Ito's lemma is applicable for continuous processes. This section will generalize to noncontinous semimartingales. 

Continous part of quadratic varations and covariations defined as

$$
\begin{align*}
[X]^c_t = & [X]_t - \sum_{s\leq t} \Delta X_s^2 \\
[X,Y]^c_t = & [X,Y]_t - \sum_{s\leq t} \Delta X_s \Delta Y_s
\end{align*}
$$

**Theorem (Generalized Ito Formula)** Let $$X=(X^1, \dots, X^d)$$ be a semimartingales such that $$X_t, X_{t-}$$ take values in an open subset. Then, for any twice differentiable functionn $$f$$, $$f(X)$$ is a semimartingales and

$$
    df(X) = D_if(X_{-})dX^i + \frac{1}{2}D_{ij}f(X)d[X^i, X^j]^c + (\Delta f(X)- D_i f(X_{-}) \Delta X^i)
$$

**Example: The Doleans exponential**
The Dolean exponential of a semimartingales $$X$$:

$$
U = 1 + \int U_{-}dX
$$

Continous part: $$d[U]^c = U_{-}d[X]^c$$ and the jumps: $$\Delta U = U_{-}\Delta X$$.

By the generalized Ito formula, 

$$
\begin{align*}
d\log (U) &= U^{-1}_{-}dU - \frac{1}{2}U^{-2}_{-} d[U]^c + (\Delta \log(U) - U^{-1}_{-}\Delta U)\\
&= dX - \frac{1}{2}d[X]^c + (\log (1 + \Delta X) - \Delta X)
\end{align*}
$$

Then we can integrate above and get the solution w.r.t. $$X$$

**Proof (Generalized Ito Formula)**

Again, we use a Taylor expansion

$$
f(X_t) = f(X_s) + D_i f(X_s)\delta X^i + \frac{1}{2}D_{ij}f(X_s) \delta X^i \delta X^j + R_{s,t}
$$

Partitioning interval $$[0, T]$$, we have

$$
f(X_T) = f(X_0) + \sum_{k=1}^n D_i f(X_{t^n_{k-1}})\delta_{n,k} X^i + \frac{1}{2} \sum_{k=1}^n D_{ij}f(X_{t^n_{k-1}})\delta_{n,k} X^i \delta_{n,k} X^j + \sum_{k=1}^n R_{t^n_{k-1}, t^n_k}
$$

While the first two integral can be derived similarly to the proof of Ito formula, the remaining term $$\sum_{k=1}^n R_{t^n_{k-1}, t^n_k}$$. 

$$
\begin{align*}
R_{s,t} = & f(X_t) - f(X_s) -D_i f(X_s) \delta X^i - \frac{1}{2}f(X_s)\delta X^i \delta X^j\\
\to & \Delta f(X_u) - D_i f(X_{u-})\Delta X_u^i - \frac{1}{2} D_{ij} f(X_{u-})\Delta X^i_u \Delta Y^i_u
\end{align*}
$$