---
layout: distill
title: Numerical methods for SDEs
description: Study some approximation methods in solving SDEs, i.e., Euler-Maruyama method, Milstein's method,...
date: 2021-11-02
---

This post summarizes some well-known numerical methods in solving stochastic differential equations (SDEs). Partial differential equations (PDEs) in general, or SDEs specifically selfdom lead to exact solution so we need to seek approximation solutions. Compared to traditional PDEs, solving SDEs requires to handle the randomness associated to the equations. In most of SDEs, we often encounter white noise or derivative of Brownian motion. Different methods will tackle with this randomness differently.

## Euler-Maruyama method

At the heart of numerical methods for differential equations, the key idea is *discretization*. The derivative is approximated as

$$\frac{dx}{dt}(t) \approx \frac{x(t + \Delta t) - x(t)}{\Delta t}$$

A simple ordinary differential equation will be converted as

$$
\frac{dx}{dt} = f(x, t) \quad \Rightarrow \quad x(t + \Delta t) = x(t) + f(x, t) \Delta
$$

Assume that we start at $x(0)$, we have to go through many step $\Delta t$ to reach $x(T)$ at time $T$. In this case, the discretization task is simple by partitioning the time interval. For 2-dimensional or 3-dimensional PDEs, there are discretization methods, for example, finite element methods, designed specifically to create meshes over domain spaces.

Now, consider a SDE

$$
dX_t = f(X_t, t) dt + g(X_t, t) dW_t
$$

The Euler-Maruyama method gives us the approximation as

$$
X(t + \Delta t) = X(t) + f(X, t) \Delta t + g(X, t) \Delta W_t
$$

Since $W_t$ is a Wiener process or a Brownian motion, the difference between to time steps is distributed as

$$
\Delta W_t = W_{t + \Delta t} - W(t) \sim \mathcal{N}(0, \Delta t)
$$

So $\Delta W_t$ will be sampled during solving the SDE and computed by $\eta \sqrt{\Delta t}$ as we sample $\eta$ from a standard normal distribution $\mathcal{N}(0, 1)$. 

The final form of sampling process for $X$ is

$$
X(t + \Delta t) = X(t) + f(X, t) \Delta t +  \eta g(X, t)  \sqrt{\Delta t}, \quad \eta \sim \mathcal{N}(0, 1).
$$

**Approximation Error Analysis**

Because of the way of discretizing, the Euler method approximates the real solution with accuracy $\mathcal{O}(\Delta t)$. 

To assess the performance of an approximate method, one considers two types of convergence

+ Strong Convergence: $\mathbb{E}[\lvert x - X \rvert] \leq C \Delta t^\gamma$, using the factor $\gamma$ to judge the approximation accuracy.
+ Weak Convergence: difference of first-order estimate $\lvert\mathbb{E}[x] - \mathbb{E}[X]\rvert \leq C \Delta t^\beta$.

The Euler-Maruyama has a strong convergence order of $1/2$ and a weak convergence of order $1$ which is an extremely slow convergence.

## Milstein's method

The Milstein's method is to improve the Euler-Maruyama by taking into account Ito's lemma. 

$$
X(t + \Delta t) = X(t) + \left(f(X,t) - \frac{1}{2} gg_x (X, t)\right) \Delta t + \sqrt{\Delta t} g(X, t)\eta + \frac{\Delta t}{2} gg_x(X, t)\eta^2
$$

Why is there a new term $gg_x(X, t) = g(X,t)\frac{\partial g}{\partial x}(X, t)$? This comes from the fact that $(dW_t)^2 = dt$ and Ito's lemma. 

**Explanation with geometric Brownian motion** 
Given that $dX_t = \mu X dt + \sigma X dW_t$, Ito's lemma for $\ln X_t$ is

$$
d \ln X_t = \left(\mu - \frac{1}{2}\sigma^2\right)dt + \sigma dW_t
$$

For an interval $[t, t + \Delta t]$, the approximated solution is derived as

$$
\begin{aligned}
X_{t + \Delta t} = & X_t \exp \left \{\int_t^{t + \Delta t}\left(\mu - \frac{1}{2}\sigma^2\right)du + \int_t^{t + \Delta t}\sigma dW_u \right\} \\
\approx & X_t \left( 1 + \left(\mu - \frac{1}{2}\sigma^2\right)\Delta t + \sigma \Delta W_t + \frac{1}{2} \sigma^2 (\Delta W_t)^2 + \mathcal{O}(t^2)\right)
\end{aligned}
$$

The last equation is the Talor expansion of $\exp(\cdot)$ where $\Delta t$ goes up to order $1$, $\Delta W_t$ goes up to order $2$. In this case, $f(X, t) = \mu X, g(X,t) = \sigma X$, resulting in $g g_x(X, t) = X\sigma^2$.

Although this is the derivation for a specific case of geometric Brownian motion, the general explanation is possible.

**Explanation for the general case** Now, going back considering the case

$$
dX_t = f(X_t, t) dt + g(X_t, t) dW_t
$$

Assume we work on a small interval $[0, h]$. And on this particular interval, $f(X_t, t) = f(X_0, 0), g(X_t,t) = g(X_0, 0)$. This leads to

$$
X_t \approx X_0 + f(X_0, 0)t + g(X_0, 0) dW_t = X_0 + g(X_0, 0) W_t + \mathcal{O}(h)
$$

On the other hand,

$$
\begin{aligned}
g(X_t, t) = & g(X_0, 0) + g_x(X_0, 0)(X_t - X_)) + \mathcal{O}(h) \\
= & g(X_0, 0) + g_x(X_0, 0)g(X_0, 0)W_t + \mathcal{O}(h)
\end{aligned}
$$

We can then obtain 

$$
S_h = S_0 + f(X_0, 0)h + g(X_0, 0)W_h + gg_x(X_0,0)\int_0^hW_tdW_t + \mathcal{O}(h^{3/2})
$$

Now, Ito calulus is used to derive $\int_0^h W_t dW_t = \frac{1}{2}W_h^2 - \frac{1}{2}h$. To this end, we can obtain the Milstein formular.

Both strong and weak convergence is of order $1$ which is better than the Euler-Maruyama method. See <a href="https://hautahi.com/sde_simulation">this</a> for a simulation comparison between the two methods

## KPS method

For a better convergence, one may look for a stronger convergence. The following is the KPS method. Advanced method can be found like <a href="https://www.sciencedirect.com/science/article/abs/pii/S016892749600027X">high-order Runge-Kutta methods</a> which, however, will not discuss here. 

The update for KPS method follows

$$
\begin{aligned}
X_{t + \Delta t} = & X_t + f\Delta t + g \Delta W_t + \frac{1}{2} gg_x ((\Delta W_t)^2 - \Delta t) \\
&+ gf_x \Delta U_t + \frac{1}{2}\left(ff_x + \frac{1}{2}g^2f_{xx}\right)\Delta t^2\\
& + \left(fg_x + \frac{1}{2}g^2gg_{xx}\right)(\Delta W_t \delta t - \Delta U_t) \\
& + \frac{1}{2}g(gg_x)_x\left(\frac{1}{3}(\Delta W_t)^3 -\Delta t\right) \Delta W_t
\end{aligned}
$$

where $\Delta W_t = \sqrt{\Delta t}\eta, \eta \sim \mathcal{N}(0,1)$ and $\Delta U_t = \int_{t}^{t + \Delta t} \int_t^s dW_s ds = \frac{1}{3}\Delta t^3 \lambda, \lambda \sim \mathcal{N}(0,1)$.

Phew! The formula is complicated. Why am I bothering writing this down?
## Adaptive timestep
If there are adaptive learning rate in machine learning, numerical methods of differential equations have ways to pick adaptive timestep instead of fixed one. This analogy does not make sense since the approach is completely different. 

The procedure consists of two steps:

1. Propose a step size and estimate the error. Here, estimating error may consider the inherence of noise
2. Accept or reject the step size according to some criteria.

A complete description is in <a href="https://www.aimsciences.org/article/doi/10.3934/dcdsb.2017133">this reference<a>.



