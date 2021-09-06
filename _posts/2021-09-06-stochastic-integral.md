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

+ $$[X]^{P_n} \to [X]$$
+ $$[X, Y]^{P_n} \to [X, Y]$$

**Theorem (Integration by Parts)** If $$X, Y$$ are semimartingales then

$$
    XY = X_0Y_0 \int X_{-} dY + \int Y_{-}dX + [X,Y]
$$