---
layout: distill
title: White noise - A more intuitive look
date: 2021-12-09
description: A further note of white noise in functional view
---
White noise is the concept being seen in various fields of science and technology. Although its definition is simply to describe chaotic randomness, it can be generalized mathematically in functional analysis, therfore, leading to consistent theory and applications like stochastic analysis.

Let's jump to the most traditional definition, $\xi$ is defined as a white noise if 

$$
\mathbb{E}[\xi_t] = 0 \quad, \quad \mathbb{E}[\xi_t\xi_s] = \delta(t - s)
$$

Here $\delta(\cdot)$ is Dirac's delta function. Even we call this function, it actually makes sense when we view it as a distribution or *generalized function*. 

$$
\int f(s)\delta(s)ds = f(0)
$$

### Functional view

Let's forget about $\delta(\cdot)$ is a function taking some real value. From now on, we consider it as a functional by taking a function as input

$$
\delta: f \to f(0)
$$

Here, $f$ is called *test function*. The idea is that a generalized function (distribution) takes a test function to measure (test) and get the outcome of the examination. Here, delta function as a distribution measures the value at a location shaply (even though measuring a infinitely sharp location is not physically realistic). 


With the above introduction of the functional approach, we may write a white noise as $\xi(f)$ with some test function $f$.  

When defining in such a way, the properties of white noise should be preserved including zero mean, $\mathbb{E}[\xi(f)] = 0$, and covariance

$$
\begin{aligned}
\mathbb{E}[\xi(f)\xi(g)] 
= & \mathbb{E}\left[\int_0^\infty f(s) \xi_s ds \int_0^\infty g(t) \xi_t dt\right] \\ 
= &\int\int f(s)g(t) \mathbb{E}[\xi_s\xi_t]dtds \\
= &\int\int f(s)g(t) \delta(t-s)dtds \\
= &\int f(t)g(t) dt \\
= &\langle f, g \rangle
\end{aligned}
$$

**Functional definition of white noise** At this point, we may define the white noise as a *random linear functional* such that $\xi(f)$ is Gaussian with 

$$
\mathbb{E}[\xi(f)] = 0 \quad, \quad \mathbb{E}[\xi(f)\xi(g)] = \langle f, g \rangle
$$

**Connection to Wiener process** We previous see 

$$\xi(f) = \int_0^\infty f(t) \xi_t dt$$

Now consider a stochastic integral with a Wiener process $W_t$

$$
\int_0^\infty f(t) dW_t
$$

One may accept (not straighforward though as Wiener process is nowhere differentiable) the fact that white noise is a derivative version of a Wiener process, therefore, $\xi_t dt = dW_t$. Now, we can cast the functional $\xi(f)$ as

$$
\xi(f) = \int_0^\infty f(t)dW_t
$$







