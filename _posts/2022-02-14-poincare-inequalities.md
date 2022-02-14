---
layout: distill
title: Markov process and Poincare inequality
date: 2022-02-14
description: How to bound the variance of a Markov dynamical system?
---

It has been a while since the last post. This post will take a fresh new topic on inequalities of dynamical systems or Markov processes specifically. All the content is based on an excellent (I think) <a href="https://web.math.princeton.edu/~rvan/APC550.pdf"> lecture note</a> lecture note from <a href="https://web.math.princeton.edu/~rvan/">Ramon Van Handel</a>. 

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


**Reversibility** 

