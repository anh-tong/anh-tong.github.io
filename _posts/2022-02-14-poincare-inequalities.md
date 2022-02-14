---
layout: distill
title: Markov process and Poincare inequality
date: 2022-02-14
description: How to bound the variance of a Markov dynamical system?
---

It has been a while since the last post. This post will take a fresh new topic on inequalities of dynamical systems or Markov processes specifically. All the content is based on an excellent (I think) <a href="https://web.math.princeton.edu/~rvan/APC550.pdf"> lecture note</a> from <a href="https://web.math.princeton.edu/~rvan/">Ramon Van Handel</a>. 

The main setup here is that we consider a high-dimensional data consisting of $X_1, X_2,..., X_n$ . We want to understand the behaviors of any function $f$ on these data when assuming $X_1,..., X_n$ are random variables. The behaviors here can be the variance of $f$ (how much the function fluctuates) or the suprema charateristics of $f$. This post will focus on the variance. 
One of classical results is that we can bound the variance of $f(X_1, ..., X_n)$ by some form of individual gradients on each dimension $1, ..., n$ (kind of hand waving for not explaining this here). 

The index sets $1, ..., n$ are discrete and finite. In this setting, we consider the infinite case $\{X\}_{t\in T}$, where $T$ usually is a continous time index. At the end of this post, we see how the variance of $f$ is bounded by gradients as in Poincare inequality.

### Makov process
The results will be established within Markov processes which are consider as **memoryless** stochastic process

$$\mathbb{E}[f(X_{t+s}| \{X_r\}_{r\leq t})] = P_sf(X_t)$$

The term **memoryless** is coined because the whole history $\{X_{r}\}_{t}$ is disregared and the expectation only is expressed by the most recent one $X_t$. 

The stationarity is defined when given a probability measure $\mu$

$$\mu(P_tf) = \mu(f)$$

This means that no matter what time it is, the measure is invariant. There are some results on stationary measures as follows:

**Lemma 1** The following hold given stationary measure $\mu$ 
1. Contraction (decreasing in norm): $\lvert\lvert P_tf \rvert\rvert_{L^p(\mu)} \leq \lvert \lvert f \rvert\rvert_{L^p(\mu)}$
2. Linearity: $P_t(\alpha f + \beta g) = \alpha P_t f + \beta P_t g$
3. Semigroup: $P_{t+s}f = P_tP_s f$
4. Conservative: $P_t 1 = 1$ a.s.

For the constraction property, we can easily prove by Jensen's inequality and the tower property $\lvert\lvert P_tf\rvert \rvert_{L^p}^p = \mathbb{E}[\mathbb{E}[(P_tf(X_0))]^p\mid X_0] =\mathbb{E}[\mathbb{E}[(f(X_t))]^p\mid X_0] \leq  \mathbb{E}[\mathbb{E}[(f(X_t))^p]\mid X_0] = \lvert\lvert f\rvert \rvert_{L^p}^p$. 

The contraction also leads to the derease of variance as $t$ increases. 

**Generator** For the case of discrete Markov processes, we often work with transition probability. However, in our case, such notion does not exist. Instead, we need to define an operator as $\mathcal{L}$ as a generator

$$
\mathcal{L}f :=\lim_{t \to 0} \frac{P_t f - f}{t}
$$

which quantify the rate of change of operator $P_t$. In particular, we have 

$$\frac{d}{dt} P_t f = \lim_{\delta \to 0} \frac{P_{t + \delta}f - P_tf}{\delta} = \lim_{\delta \to 0} P_f(\frac{P_\delta f - f}{\delta}) = \lim_{\delta \to 0}\frac{P\delta P_t f - P_tf}{\delta} = P_t\mathcal{L}f = \mathcal{L}P_tf$$

This provides the commutative property between $P_t$ and $\mathcal{L}$. 


**Reversibility** This is a rebranding term of self-adjoint where $\langle f, P_t g \rangle = \langle P_t, g\rangle$. However, the implication here is that there is a backward process having the same law:

$$
\langle \textcolor{red}{P_t f}, g \rangle = \langle f, P_t g \rangle = \mathbb{E}[ f(X_0) \mathbb{E}[g(X_t)|X_0]] = \mathbb{E}[f(X_0) g(X_t)] = \mathbb{E}[\textcolor{red}{\mathbb{E}[f(X_0)|X_t]} g(X_t)]
$$
By the defition, the red terms lead to $P_t f(x) := \mathbb{E}[f(X_t)|X_0=x] = \mathbb{E}[f(X_0)|X_t=x]$. This is why we call it *reversibility*.


**Note** We can see many case studies, i.e., solution of stochastic differential equations (SDEs) satisfy the above definitions and properties. So it can be useful to analyze recent models in machine learning, e.g.,  Neural SDEs or score-based models, that attract a lot attention.

**Egordicity** This notion usually is encountered when studying dynamical systems which converge to stationary state no matter what initial values are. That is, $P_tf \to \mu f$ in $L^2(\mu)$ as $t\to 0$.

Before going to the main result, it is necessary to define one more concept which is Dirichlet form $\mathcal{E}(f, g)$

$$\mathcal{E}(f, g) = - \langle f, \mathcal{L}g\rangle$$

**Theorem** Let $P_t$ be a reversible ergodic Markov semigroup with stationary measure $\mu$. The following are equivalent:

1. $Var_\mu[f] \leq c\mathcal{E}(f, f)$ for all $f$ (<span style="color:red">Poincare inequality</span>)
2. $\lvert \lvert P_tf -\mu f \rvert \rvert_{L^2(\mu)} \leq e^{-t/c} \lvert \lvert f - \mu f \rvert \rvert_{L^2(\mu)}$
3. $\mathcal{E}(P_tf, P_tf)\leq e^{-2t/c}\mathcal{E}(f, f)$
4. $\lvert \lvert P_tf -\mu f \rvert \rvert_{L^2(\mu)} \leq \kappa(f)e^{-t/c}$
4. $\mathcal{E}(P_tf, P_tf) \leq \kappa(f)e^{-t/c}$

**Poincare inequality**

It is surprised that we can capture the dynamic of variance by a differential equation. This is the starting point of the proof. 

**Lemma** We have the identity of 
$$\frac{d}{dt}Var_{\mu}[P_tf]=-2\mathcal{E}(P_tf, P_tf)$$

Proof:

$$
\begin{aligned}
\frac{d}{dt}Var_\mu[P_tf] = & \frac{d}{dt}\{\mu((P_tf)^2) - (\mu P_tf)^2\} && \\
= & \frac{d}{dt} \mu((P_tf)^2) && ( \mu(P_tf) = \mu(f) \text{does not depend on }t)\\
= & \mu(2P_tf \frac{d}{dt}P_tf) &&\\
= & \mu(2P_tf\mathcal{L}P_tf) && \\
= & -2 \mathcal{E}(P_tf, P_tf) && (\text{by definition of Dirichlet form})
\end{aligned}
$$

As the previous observation that $t \mapsto Var_\mu[P_tf]$ is a decrease function, then $\mathcal{E}(f, f) = -\frac{1}{2}\frac{d}{dt}Var_\mu[P_tf]\rvert_{t=0} \geq 0$.

Also by the egordicity $P_tf \to \mu f$ then $Var_\mu[P_tf] \to Var_\mu[\mu f] = 0$. Actually the variance can be written as the integration (solution) of above differential equation.

$$Var_{\mu}[f] = \int_\infty^0 \frac{d}{dt}Var_{\mu}[P_tf]dt=2\int_0^\infty \mathcal{E}(P_tf, P_tf)$$

**<span style="color:red">(3 $\Rightarrow 1$): Assumming 3 satisfies, proving 1</span>** By 3, we have $\mathcal{E}(P_tf, P_tf)\leq e^{-2t/c}\mathcal{E}(f, f)$. Putting this into the integral

$$Var_{\mu}[f] = 2 \mathcal{E}(f, f)\int_0^\infty e^{-2t/c}dt = c\mathcal{E}(f,f)$$

**<span style="color:red">(1 $\Rightarrow 2$): Assumming 2 satisfies, proving 1</span>** By assuming 1, we have $c \mathcal{E}(P_tf, P_tf) \geq Var_\mu[P_tf]$. Putting this into the variance identities

$$
\frac{d}{dt}Var_\mu[P_tf]  \leq -\frac{2}{c} Var_\mu[P_tf]
$$
As we all know that the solution of $\frac{d}{dt}x = a x$ is $x_t = x_0 e^{at}$. Then $Var_\mu[P_tf] \leq Var_\mu[P_0f]e^{-2t/c}$ which is further expanded as

$$\lvert\lvert P_tf - \mu f \rvert \rvert_{L^2{\mu}}^2 =Var_\mu[P_tf] \leq Var_\mu[P_0f]e^{-2t/c} =  Var_\mu[f]e^{-2t/c} = e^{-2t/c} \lvert \lvert f-\mu f \rvert\rvert_{L^2(\mu)}^2$$

It is not difficult to show (2 $\Rightarrow$ 1) by using the variance identity.

The rest of equivalence requires to take into account the egordicity that we have another identity.

**Lemma** If the Markov semigroup $P_t$ is reversible, then $t \mapsto \log Var_\mu[P_t f]$ and $t \mapsto \log \mathcal{E}(P_tf, P_tf)$ are convex.

The main technique to prove the convexity here is to show the Hessian is nonnegative. Luckly, we can derive such Hessian information. The first-order derivative is

$$
\begin{aligned}
\frac{d}{dt}\mathcal{E}(P_tf, P_tf) & = -\frac{d}{dt} \langle P_tf, \mathcal{L} P_tf\mathcal \rangle_\mu && (\text{by definition of Dirichlet form}) \\
& = -\langle \frac{d}{dt} P_tf,  \mathcal{L} P_tf\mathcal \rangle_\mu - \langle  P_tf,  \frac{d}{dt} \mathcal{L} P_tf\mathcal \rangle_\mu&& (\text{derivative of inner product}) \\
& = -\langle \mathcal{L} P_tf,  \mathcal{L} P_tf\mathcal \rangle_\mu - \langle  P_tf,  \mathcal{L}^2 P_tf\mathcal \rangle_\mu&& (\text{by definition of generator}) \\
& = -2 \lvert \lvert  \mathcal{L} P_tf \rvert \rvert_{L^2(\mu)}^2 && (\mathcal{L} \text{ is self-adjoint})
\end{aligned}
$$

This will allow us to obtain

$$
\begin{aligned}
\frac{d^2}{dt^2}\log Var_\mu[P_tf] &= \frac{d}{dt}\left(\frac{1}{Var_\mu[P_tf]}\frac{d}{dt}Var_\mu[P_tf]\right) && \\
& = \frac{d}{dt}\left(\frac{1}{Var_\mu[P_tf]} \times (-2) \mathcal{E}(P_tf, P_tf)\right) && (\text{by the variance identity})\\
& = \frac{4\lvert \lvert  \mathcal{L} P_tf \rvert \rvert_{L^2(\mu)}^2}{Var_\mu[P_tf]} - \frac{4\mathcal{E}(P_tf, P_tf)}{Var_\mu[P_tf]^2} && (\text{derivative of product and the above result})\\
& = \frac{4}{Var_\mu[P_tf]^2}\left\{Var_\mu[P_tf] \lvert \lvert  \mathcal{L} P_tf \rvert \rvert_{L^2(\mu)}^2 - \langle P_tf, \mathcal{L}P_tf \rangle_\mu^2\right\}
\end{aligned}
$$

The nonnegativity of the right hand side is derived from the fact that $\mathcal{L}$ is self-adjoint, $\mathcal{L}1 = 0$ and Cauchy-Schwarz inequality

$$
\begin{aligned}
\langle P_tf, \mathcal{L}P_t f \rangle_\mu^2 =& (\langle P_tf, \mathcal{L}P_t f \rangle_\mu - \underbrace{\langle \mathcal{L} \mu f, P_tf \rangle}_{0})^2 && \\
= & (\langle P_tf, \mathcal{L}P_t f \rangle_\mu - {\langle  \mu f, \mathcal{L}P_tf \rangle})^2 && (\mathcal{L} \text{ is self-adjoint})\\
= & \langle P_tf - \mu f, \mathcal{L}P_t f \rangle_\mu^2 && \\
\leq & \lvert \lvert  P_tf - \mu f \rvert \rvert_{L^2(\mu)}^2\lvert \lvert  \mathcal{L} P_tf \rvert \rvert_{L^2(\mu)}^2 && (\text{Cauchy-Schwarz inequality})\\
= & Var_\mu[P_tf] \lvert \lvert  \mathcal{L} P_tf \rvert \rvert_{L^2(\mu)}^2
\end{aligned}
$$

This makes the Hessian nonnegative. Therefore, we can conclude about the convexity of $t \mapsto \log Var_\mu[P_tf] $. For the case $t \mapsto \log \mathcal{E}(P_tf, P_tf)$, we can obtain the same conclusion but with the inequality $\mathcal{E}(f, g)^2 \leq \mathcal{E}(f, f)\mathcal{E}(g, g)$ from the fact that $\mathcal{E}(f + tg, f+tg) \geq 0$.

**<span style="color:red">(2 $\Rightarrow 3$): Assumming 2 satisfies, proving 1</span>** As 2 is true. This means $\lvert \lvert P_tf -\mu f \rvert \rvert_{L^2(\mu)} \leq e^{-t/c} \lvert \lvert f - \mu f \rvert \rvert_{L^2(\mu)}$.

From the convexity of $t \to \log Var_\mu[P_tf]$, the first-order derivative function 

$$
t \mapsto \frac{d}{dt} \log Var_\mu[P_tf] = {\frac{1}{Var_\mu[P_tf]} \frac{d}{dt}Var_\mu[P_tf] } = \frac{-2 \mathcal{E}(P_tf, P_tf)}{Var_\mu[P_tf]}
$$

 is an increasing function. Therefore, 

 $$
 \frac{-2 \mathcal{E}(P_tf, P_tf)}{Var_\mu[P_tf]} \geq \frac{-2 \mathcal{E}(P_0f, P_0f)}{Var_\mu[P_0f]} = \frac{-2 \mathcal{E}(f, f)}{Var_\mu[f]}
 $$

 This leads to

 $$
 \frac{\mathcal{E}(P_tf, P_tf)}{\mathcal{E}(f, f)} \leq \frac{Var_\mu[P_tf]}{Var_\mu[f]} = \frac{\lvert \lvert P_tf -\mu f \rvert \rvert_{L^2(\mu)}^2}{\lvert \lvert f - \mu f \rvert \rvert_{L^2(\mu)}^2} \leq e^{-2t/c}
 $$

The remaining proof for other implication is derived similarly.

### Conclusion
This post studies the inequality involves the variance of dynamically systems. As the beginning of the post, the variance will be bounded by gradient but in fact, we find the bound in Dirichlet form. However, this form will be coresponding to gradient information. For example, in the particular case (Ornistein-Uhlenbeck process) of $P_tf(x) = \mathbb{E}[f(e^{-t}x + \sqrt{1 - e^{-2t}}\xi)], \xi\sim \mathcal{N}(0,1)$, the $\mathcal{E}(f, g) = \langle f', g'\rangle_\mu$.

I anticipate that such inequalities can be useful for understanding any quantities, e.g. $f$ as a likelihood function, related to  Neural SDE, or score-based generative models. The variance identities somehow resembles to the continous normalizing flow models where the log-density funcion is also governed by a differential equation.
