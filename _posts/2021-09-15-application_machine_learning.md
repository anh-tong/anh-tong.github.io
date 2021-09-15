---
layout: distill
title: Applications of Stochastic Calculus in Machine Learning
description: Exploring some aspect of stochastic calculus in optimization. The blog is based on the slides of Prof. Maxim Raginsky at UIUC. 
date: 2021-09-15
bibliography: 2021-09-15-application-machine-learning.bib
---

## Applications in machine learning

Now, let's talk about what cases we can apply techniques of stochastic calculus to machine learning. Just like financial data, if a machine learning model deals with time series, considering stochastic calculus to handle randomness is a promising direction. Stochastic calculus can also come to improve and provide insights for machine learning methods. 

This section will  focus on presenting the connection between stochastic optimization and stochastic calculus. The content of this section follows closely <a href="http://maxim.ece.illinois.edu/pubs/columbia.pdf">the slides</a> by Maxim Raginsky. 

Stochastic optimization is one of the most well-known methods in machine. The method tries to miminizing a function by updating the function parameters in the inverse direction of its gradient. It does not have access to the full gradient but a noisy gradient which is usually computed from a small bactch of data. So because of this noisy gradient, stochastic calculus probably is a right tool.

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

Studing the dynamic of gradient descent methods has been seen in some work including Neural Tangent Kernel <d-cite>neural_tangent_kernel</d-cite>
<!-- TODO: A related topic is Neural Tangent Kernel but no stochaticity is considered  -->

<!-- TODO: Diffusion process -->
<!-- TODO: Kolmogorov equation: constructing diffusion process -->





