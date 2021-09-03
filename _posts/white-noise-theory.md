---
layout: distill
title: White Noise Theory
date: 
description: An introduction of white noise theory
---

### Introduction
Recently, I have picked up some background of white noise theory after ready this paper <d-cite><\d-cite>. White noise theory developed by Hida generalizes the white noise in functional views. 

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

+ Let $$\mathcal{S}(\mathbb{R})$$ denote the Schwartz space of rapidly decrease smooth function on $$\mathbb{R}$$ and 
+ let $$\Omega = \mathcal{S}'(\mathbb{R})$$ be its dual (or *space of tempered distributions*). 
+ Let $$\mu$$ be the probability measureon the Borel sets $$\mathcal{B}(\mathcal{S}'(\mathbb{R}))$$. If 

$$
    \int_{\mathcal{S}'(\mathbb{R})} \exp(i \langle \omega, f \rangle) \mu d\omega = \exp \left(-\frac{1}{2}\lVert f \rVert^2_{L^2(\mathbb{R})}\right),
$$
then the measure $$\mu$$ is called the white noise probability measure. 

We have the following properties:

+ The expectation $$\mathbb{E}[\langle \omega, f\rangle] = 0$$
+ And $$\mathbb{E}[\langle \omega, f\rangle^2] = \lVert f \rVert_{L^2(\mathbb{R})}$$

### Brownian motion case
We can see that Brownian motion can fit under the definition of white noise theory.