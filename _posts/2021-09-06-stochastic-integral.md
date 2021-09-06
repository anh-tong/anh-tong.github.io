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

