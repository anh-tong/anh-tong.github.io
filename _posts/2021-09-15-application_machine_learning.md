---
layout: distill
title: Applications of Stochastic Calculus in Machine Learning
description: Exploring some aspect of stochastic calculus in optimization. The blog is based on the slides of Prof. Maxim Raginsky at UIUC. 
date: 2021-09-15
bibliography: 2021-09-15-application-machine-learning.bib
---

Now, let's talk about what cases we can apply techniques of stochastic calculus to machine learning. Just like financial data, if a machine learning model deals with time series, considering stochastic calculus to handle randomness is a promising direction. Stochastic calculus can also come to improve and provide insights for machine learning methods. 

This section will  focus on presenting the connection between stochastic optimization and stochastic calculus. The content of this section follows closely <a href="http://maxim.ece.illinois.edu/pubs/columbia.pdf">the slides</a> by Maxim Raginsky. 

Stochastic optimization is one of the most well-known methods in machine learning. The method tries to miminizing a function by updating the function parameters in the inverse direction of its gradient. It does not have access to the full gradient but a noisy gradient which is usually computed from a small bactch of data. So because of this noisy gradient, stochastic calculus probably is a right tool.

<!-- TODO: the slides seems focusing on gradient descent -->

Formally, machine learning problems often end up with miminizing

$$
F(x) = \mathbb{E}_\xi[f(x, \xi)]
$$

where the randomness presented by $$\xi$$ comes from randomized batch generations. The next procedure is to take a series of stochastic gradient steps to reach to a (local) minima. Although these steps are discrete, we can generalize with a continous version where the evolution of the parameters can follow the following dynamic:

### Background of stochastic calculus for this section

$$
\frac{\text{d}X_t}{\text{d}t} = G(X_t, t, \omega)
$$

where $$G$$ stands for a function computing gradients and is injected with a random variable $$\omega$$. 

Studing the dynamic of gradient descent methods has been seen in some work including Neural Tangent Kernel<d-cite key="neural_tangent_kernel"> </d-cite>. 

#### Diffusion process

A diffusion process is defined as a Markov process if it satisfies

+ (i) $$p(\lVert X_{t+h} - X_t \rVert > r \mid X_t = x) = o(h),$$
+ (ii) $$\mathbb{E}[(X_{t+h} - X_t) \mathbb{1}_{\{\lVert X_{t+h} - X_t \rVert \leq r\}} \mid X_t = x] = hb(x) + o(h),$$
+ (iii) $$\mathbb{E}[(X_{t+h} - X_t)(X_{t+h} - X_t)^\top \mathbb{1}_{\{\lVert X_{t+h} - X_t \rVert \leq r\}} \mid X_t = x] = hA(x) + o(h),$$
for some $$b(\cdot) \in \mathbb{R}^d, A(\cdot) = A^\top (\cdot) \in \mathbb{R}^{d\times d}_+$$.

The above properties can intuitively interpreted as that there exists a local drift with amount of $$hb(x) + o(h)$$ and a covariance matrix as local diffusion matrix $$hA(x) + o(h)$$. 


#### Kolmogrov equation: Constructing diffusion process

**Theorem (Kolmogorov equation)** Let $$b, A$$ satisfy a "certain condition", then there is a diffusion process $$(X_t)_{t\geq 0}$$, such that, for any $$f \in C^2$$, 

$$
\mathbb{E}[f(X_t)] = \mathbb{E}[f(X_0)] + \int_0^t \mathbb{E}[\mathcal{L} f(X_s)] \text{d}s,
$$

where,

$$
\mathcal{L}f(x) = b(x)^\top \nabla f(x) + \frac{1}{2} \text{tr}[A(x) \nabla^2 f(x)]\text{d}s
$$

*Example of Brownian motion* 

As we know that Brownian motion $$W_t$$ has zero mean ($$b=0$$) and covariance $$A = \mathbf{I}$$, we can have the expectation

$$
\mathbb{E}[f(W_t)] = f(0) + \frac{1}{2}\mathbb{E}[\text{tr}(\nabla^2 f(x))]
$$

We shall see next that the parameters going through optimization trajectory will follow a stochastic process (diffusion process, to be exact), we are interested in understanding the output of this process through a function $$f$$ in order to compare to optimum value.

### Tackle local optima

One way to somehow escape local mimina is to add a random/jitter to the gradient descent step

$$
x_{t + \text{d}t} = x_t - \nabla F(x_t) \text{d}t \quad \Rightarrow \quad X_{t+\text{d}t} \sim \mathcal{N}(x_t -\nabla F(x_t)\text{d}t, \textcolor{red}{(2/\beta \cdot \text{d}t) \mathbf{I}_d})
$$

The red term can be further generalized with Brownian motion, leading to a noisy gradient descent:

$$
X_{t + \text{d}t} = X_t - \nabla F(X_t)\text{d}t + \textcolor{red}{\sqrt{2/\beta} (W_{t + \text{d}t} - W_t)}
$$

And now, we can recognize something familiar to the Black-Scholes models. The equation here is called the Langevin diffusion which already have a rich literature in physics, Bayesian inference, MCMC. 

### Key result

Now, let's go over the main result presented in this paper<d-cite key="key_result"> </d-cite>. 

**Theorem** With a "reasonable assumption" (smoothness, dissiparity) that 

$$
\lVert \nabla F(x) - \nabla F(x') \rVert \leq M \lVert x - x' \rVert \quad, \quad x^\top \nabla F(x) \geq m \lVert x \rVert^2 - b
$$

Then,

$$
\mathbb{E}[F(X_t)] - \inf_x F(x) \leq \sqrt{c_{\text{LS}} D(\nu_0 \lVert \pi)} \exp(-t/\beta c_{\text{LS}}) + \frac{d}{\beta} \log \frac{\beta + 1}{d}
$$

where, 

+ (i) $$\nu_0 = \mathcal{L}(X_0)$$ which is the intial distribution
+ (ii) $$D(\cdot \lVert \cdot)$$ is the Kullback-Leibler distribution
+ (iii) $$c_{\text{LS}}$$ is the log-Sobolev constant of $$\pi$$

*How to intepret this theorem?* 
Well, recall that the minimum value is $$\inf_x F(x)$$. We need to compare the optimum value with the expectation of $$F(X_t)$$ at time $$t$$. The expectation is necessary since we are working with stochastic process $$X_t$$. 
So the above result is saying that the different between the value of the function evaluated over the process $$X_t$$ and the minimum is *bounded*. 

*What can we say about the bound here?* 
Looking at the right-hand side, we can see that the bound decreases *exponentially* as the time $$t$$ goes. This is quite good, proving that optimization converges very fast. Also, the second term of the right-hand side, $$\frac{d}{\beta}\log \frac{\beta + 1}{d}$$, suggests that we may select $$\beta$$  not too large as well as not too small.





