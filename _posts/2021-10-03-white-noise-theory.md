---
layout: distill
title: White Noise Theory
date: 2021-09-06
description: An introduction of white noise theory
bibliography: white-noise.bib
---

### Introduction
Recently, I have picked up some background of white noise theory after ready this paper <d-cite key="multifractional"></d-cite>. White noise theory developed by Hida generalizes the white noise in functional views. 

Starting from a classical results for a Browian montion, $$B_t$$, the following holds

$$dB_t = (dt)^2$$

This result leads to a new branch of calculus, *stochastic calculus* or *Ito calculus*. One of prominent lemmas is Ito's lemma which is considered as a chain rule to compute the derivative of a function, $$f(t, B_t)$$. A simple way to intepret Ito's lemma is to use Talor approximation up to second order and then obtain

$$df(t, B_t)=\left(\frac{\partial f}{\partial t} +\frac{1}{2}\frac{\partial^2 f}{\partial x^2}\right)dt + \frac{\partial f}{\partial x}dB_t$$

Now, what if the stochastic process here is *not* a Brownian motion? How do we do stochastic calculus for this case?

### Generalize with characteristic function

Let us start with a simple example of characteristic function of a univarite Normal random variable, $$X \sim \mathcal{N}(0, 1)$$. The characteristic function is under the form

$$
    \varphi(t) = \mathbb{E}[\exp(itX)] = \exp\left(-\frac{1}{2}t^2\right)
$$

Extending to finite dimesion where we have to deal with isotropic multivariate Gaussian distribution, the characteristic function is 

$$
    \varphi(t) = \mathbb{E}[\exp(i\langle t, X \rangle)] = \exp\left(-\frac{1}{2}\lVert t \rVert^2\right)
$$

where $$t = [t_1, \dots, t_n]^\top$$ and $$\lVert t\rVert = \sqrt{t_1^2 +\dots, t_n^2}$$. Here the inner product $$\langle x, y \rangle = x_1y_1 + \dots + x_ny_n$$. 

Obviously, this case is equivalent to Gaussian white noise with finite sample. However, stochastic process can be defined over a contiuous index set. It is natural to generalize even more. 

**Definition (White noise probability measure)** 

+ Let $\mathcal{S}(\mathbb{R})$ denote the Schwartz space of rapidly decrease smooth function on $\mathbb{R}$ and 
+ Let $\Omega = \mathcal{S}'(\mathbb{R})$ be its dual (or *space of tempered distributions*). 
+ Let $\mu$ be the probability measureon the Borel sets $\mathcal{B}(\mathcal{S}'(\mathbb{R})).$ If 

$$
    \int_{\mathcal{S}'(\mathbb{R})} \exp(i \langle \omega, f \rangle) \mu d\omega = \exp \left(-\frac{1}{2}\lVert f \rVert^2_{L^2(\mathbb{R})}\right),
$$

then the measure $\mu$ is called the white noise probability measure. 


The Lévy process also is defined based on its characteristic function in <a href="https://en.wikipedia.org/wiki/L%C3%A9vy_process">Lévy-Khintchine formula</a>.

We have the following properties:

+ The expectation $$\mathbb{E}[\langle \omega, f\rangle] = 0$$
+ And $$\mathbb{E}[\langle \omega, f\rangle^2] = \lVert f \rVert_{L^2(\mathbb{R})}$$

### Brownian motion case
We can see that Brownian motion can fit under the definition of white noise theory.

$$
    \chi_{[0, t]}(s)=\begin{cases} 1 & \text{ if } 0 \leq s \leq t\\
    - 1 &\text{ if } t \leq s \leq 0 \\
    0 &\text{ otherwise}
    \end{cases}
$$

We can define $$\tilde{B}_t=\langle \omega, \chi_{[0, t]}(\cdot)\rangle$$. Furthermore, we can say the $$\tilde{B}_t$$ is a Gaussian process with zero mean and covariance

$$
\mathbb{E}[\tilde{B}_t, \tilde{B}_s] = \min(t,s).
$$

This is exactly the definition of Brownian motion. We can verify this by examining the characteristic function

$$
\begin{align*}
\mathbb{E}\left[\exp(i \sum_{j=1}^n c_j\tilde{B}_{t_j} )\right] = & \mathbb{E}\left[\exp\left(i \langle \omega, \sum_{j=0}^n c_j\chi_{[0, t_j]}  \rangle \right) \right] = \exp \left(-\frac{1}{2}\lVert \sum_j c_j\chi_{[0, t_j]}\rVert^2 \right) \\
=& \exp\left(-\frac{1}{2}\sum_{i,j}c_i c_j\int \chi_{[0, t_i]}(s)\chi_{[0, t_j]}(s)ds\right) \\
=& \exp\left(-\frac{1}{2}\sum_{i,j}c_i c_j \min(t_i, t_j)\right)
\end{align*}
$$

This is the charateristic of a multivariate Gaussian distribution.

## Fractional Brownian Motion (fBm)

The ovariance function of fBm is

$$
k(s, t) = |t|^{2H} + |s|^{2H} - |t-s|^{2H}
$$

### Conclusion
Although the mathematical formulation presented aboved is elegant, having applications in finance <d-cite>multifractional</d-cite>, it is not clear if there is any implication yet. One potential direction is to use in generative model for time series where Brownian motion is the main source of random noise. 