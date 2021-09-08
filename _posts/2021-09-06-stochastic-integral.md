---
layout: distill
title: Stochastic Integral
date: 2021-09-06
description: Note collection of Stochastic Integral
---

### Introduction

This note is to summarize the stochastic integral of <a href="https://almostsuremath.com/stochastic-calculus/">AlmostSure's blog</a>.

By the Riemann-Stieltjes integral $$\int g df$$ is well-defined if $$g$$ is continuous and $$f$$ is **differentiable**. However, stochastic processes do not always satisfy the differentiation condition, for example, Brownian motion which is nowhere differentiable. Therefore, we need new way to define integral involving stochastic process.

The stochastic integration proposed by Kiyoshi Ito define integrals for stochastic process including adapted processes then extending to martingales and semimartingales. The integral is in fact defined via Lebesgue  sense (or <a href="https://en.wikipedia.org/wiki/Dominated_convergence_theorem">dominated convergence theorem</a>), i.e,

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

