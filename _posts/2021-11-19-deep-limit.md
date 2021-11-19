---
layout: distill
title: Theoretical aspect of variational infrence for Neural SDEs
descriptions: Some connections between stochastic optimal control and variational inference
date: 2021-11-19
---

## Introduction
In this note, I will a short review for a part of <a href="https://arxiv.org/abs/1903.01608">this paper</a>. I will try to bring (learn) some necessary background of stochastic optimal control. 

The main object discussed shortly in the following is represented as a SDE

$$
dX_t = b(X_t, t)dt + dW_t
$$

## Stochastic control problems

### Background of stochastic optimal control

Let's consider a determistic control problem first

$$
dx_t = F(x_t, u_t)dt
$$

where $x_t$ is the state variable, $u_t$ is the control variable. The optimal control problem tries to mimimize a value function

$$
V(x_t, t) = \int_t^T C(x_t, u_t) dt + D(x_T)
$$

where $C$ is the control cost function and $D$ is the cost at the terminal time $T$. In fact, the value function here can be approximated with a small change of time, $dt$.

$$
V(x_t, t) = \min_u \left\{C(x_t, u_t) + V(x_{t + dt}, t + dt)\right\}, \quad V(x, T) = D(x)
$$

This result has a long history and is known as the Hamilton-Jacobian-Bellman equation in dynamic programming. The right-hand side is further approximated with Taylor expansion. 

$$
\frac{\partial V}{\partial t} + \min_u\left\{C(x_t, u_t) + \frac{\partial V}{\partial x} F(x_t, u_t)\right\} = 0
$$

This is a ODE. However, it is nontrivial to solve this because it includes a minimization problem which we do not know exactly how to optimize it.

Now, turn our attention with the extension of the above where we consider a stochastic version

$$
dX_t = b(X_t, u_t)dt + \sigma(X_t, u_t)dW_t
$$

and then value function here is

$$
V(X_t, t) = \mathbb{E}\left[\int_t^T C(X_t, u_t) dt + D(X_T)\right]
$$

Similarly, as we apply Ito's rule when approximate $V(X_{t + dt}, t + dt)$ (just remember that second-order derivative involves here), we can derive

$$
\frac{\partial V}{\partial t} + \min_u\left\{C(x_t, u_t) + \frac{\partial V}{\partial x} F(x_t, u_t) + \frac{1}{2} \sigma^2(X_t, u_t) \frac{\partial^2 V}{\partial x^2}\right\} = 0, \quad V(x, T) = D(x)
$$

Again, this is difficult to solve in general.

### The stochastic control problem in the paper

The paper restricts the SDE with constant diffusion function

$$
dX_t = b(X_t, t) dt + dW_t, \quad t\in [0, 1], X_0 = x_0
$$

The corresponding control SDE being studied is

$$
dX_t^u = (b(X^u_t, t) + u(X^u_t, t)) dt + dW_t, \quad t\in [0, 1], X_0^u = x_0
$$

and the value function here will be denoted as $J$

$$
J(x, t) = \mathbb{E}\left[\int_t^1 C(X_s^u, u_s) ds + D(X_1^u) \mid X_t^u=x\right] 
$$

With the above derivation in the previous section, we obtain

$$
\frac{\partial J}{\partial t} + \min_u\left\{C(x, u) + (b + u) \frac{\partial J}{\partial x} + \frac{1}{2}\frac{\partial^2 J}{\partial x^2}\right\} = 0
$$

Moving terms around we obtain

$$
\frac{\partial J}{\partial t} + \mathcal{L}_tJ = -\min_u \left\{ C(x, u) + u \frac{\partial J}{\partial x}\right\}
$$

In the paper, the control cost function is the norm of $u$, therefore, the solution is exact and $u(x, t) = \frac{1}{2}\frac{\partial J}{\partial x}$, resulting

$$
\frac{\partial J}{\partial t} + \mathcal{L}_tJ = \frac{1}{2}\lvert\lvert \frac{\partial J}{\partial x} \rvert\rvert^2
$$

Let $h(x, t) = \mathbb{E}[D(X_1)|X_t = x]$ is the value function of uncontrolled SDE, then

$$
\frac{\partial h}{\partial t} + \mathcal{L_t}h = 0
$$

If we pick $J(x,t) = -\log h(x, t)$, we can obtain the exact PDE for $J$. The we can say the two value functions are the same

$$
\underbrace{-\log \mathbb{E}[D(X_1)|X_t=x]}_{ \text{uncontrolled SDE value function}} = \underbrace{\min_u \mathbb{E} \left[\int_t^1 C(X_s^u, u_s) ds + D(X_1^u) \mid X_t^u=x\right] }_{\text{controlled SDE value function}}
$$








