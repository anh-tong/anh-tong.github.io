---
layout: distill
title: Semimartingales
description: Note on semimartingales
date: 2021-10-20
---
Simply, the definition is
<p style="text-align: center;">Semimartingale = local martingale + finite variation</p>

The importance of this concept is that it enables us to define stochastic integral in a more general sense. The local martingale part will be treated using integration with Brownian motion.

## Semimartingales

**Formal definition** A regular right-continuous with left limits adapted process $S(t)$ is *semimartingale* if it can be represented as a sum of two processes:

+ local martingale $M(t)$
+ and a process of finite variation $A(t)$

$$
S(t) = S(0) + M(t) + A(t)
$$

**Example of semimartingales** It can be $S(t)=B^2(t)$, Poisson process, a diffusion which is a solution to a stochastic differential equation w.r.t. Brownian motion.

## Integrals with semimartingales

The goal here is to compute

$$
\int_0^T H(t)dS(t)
$$

Taking advantage of the decomposition of semimartingale, the integral can be obtained as the sum of two integrals where the first $\int H(t) dM(t)$ uses the integral of local martingales and the second $\int H(t) dA(t) $ uses the Stieljes integral. 

If $M(t)$ is a Brownian motion, the work is simple. But for the general case, $M(t)$ is a local martingale, we need to deal with jumps if it has.

### Local martingale part

Like the Brownian case, we start with the simple process

$$
H(t) = H(0) I_0 + \sum_{i=0}^{n-1} H_i I_{(T_i, T_{i+1}]}(t)
$$

The integral now is the sum

$$
\int_0^T H(t) dS(t) = \sum_{i=0}^{n-1} H_i\left(M(T_{i+1}) - M(T_i)\right)
$$

Now, we see the expression which is much related to quadratic variation, and all the properties evolve arount it.

### Finite Variation part

The variation of $A(t)$ is finite, then

$$
\int_0^T \lvert H(t) \rvert dV_A(t) < \infty
$$

**Note** The decomposition of a semimartingale is not unique. So can the integral results differently? The answer is no. The integral is still unique because when considering another representation of decomposition, we have $A(t)-A_1(t)= M_1(t) - M(t)$ is a local martingale, then take integral we can see the integral is the same.

### Properties of Integral with respect to Semimartingales

$X(t)$ is a semimartingale, $H(t)$ is predictable process, the integral is

$$
(H \cdot X)(t) = \int_0^t H(s) dX(s)
$$

This integral has the following properties

- Jump: If $X(t)$ has a jump, i.e. $\Delta X(t)$ , the jump of integral is $\Delta (H \cdot X)(t) = H(t) \Delta X(t)$
- Stopping time: Transfer from integral to semimartingales

$$
\int_0^{t \wedge \tau} H(s)dX(s) = \int_0^t H(s) I(s \leq \tau) dX(s) = \int_0^t H(s)dX(t \wedge \tau)
$$

- Associativity: $K \cdot (H \cdot X) = (KH) \cdot X$

## Ito's Formula for Continuous Semimartingale

With $X(t)$ is a continuous semimartingale and $f$ is twice continuously differentiable, $Y(t) = f(X(t))$ is a semimartingale and 

$$
f(X(t)) - f(X(0)) = \int_0^t f'(X(s))dX(s) + \frac{1}{2} \int_0^t f''(X(s))d[X, X](s)
$$

In differential form, it is

$$
df(X(t)) = f'(X(t))dX(t) + \frac{1}{2}f''(X(t))d[X, X](t)
$$

If the quadratic variation $ [X,X] (t)$ equals $0$, then it ends up just like ordinary calculus. If $X(t)$ is a Brownian motion, $ [X, X] (t) = t$

## Ito's Formula for Semimartingales

With $X(t)$ is a semimartingale, $f \in C^2$

$$
\begin{aligned}
f(X(t)) - f(X(0)) = & \int_0^t f'(X(s-))dX(s) + \frac{1}{2}\int_0^t f''(X(s-))d[X,X] (s) + \\
& \sum_{s\leq t} \left(\Delta f(X(s)) - f'(X(s-))\Delta X(s) -\frac{1}{2}f''(X(s-))(\Delta X(s))^2\right)
\end{aligned}
$$

where $\Delta f(X(s)) = f(X(s)) - f(X(s-))$. So why does this look a little complicate? Well, there are possible jumps in the semimartingales. And the quadratic variation of the jump part has jumps $\Delta [X,X] (s) = (\Delta X(s))^2$. The above formula can be reduced to

$$
\begin{aligned}
f(X(t)) - f(X(0)) = & \int_0^t f'(X(s-))dX(s) + \frac{1}{2}\int_0^t f''(X(s-))d[X,X]^c (s) + \\
& \sum_{s\leq t} \left(\Delta f(X(s)) - f'(X(s-))\Delta X(s)\right)
\end{aligned}
$$

## Final remark
This is a simple note on how stochastic calculus is done with semimartingales. Most of the work on stochastic differential equations stops at the randomness assumption being semimartingale. Still, there are more advanced theories, for example, <a href="https://almostsuremath.com/2016/10/21/the-projection-theorems/"> the projection theorem </a> or <a href="https://en.wikipedia.org/wiki/Rough_path"> rough path </a> to deal with subjects beyond semimartingales.
