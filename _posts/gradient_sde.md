---
layout: distill
title: Scalable Gradients for SDEs
description: A scalable methods for neural SDEs
date: 
bibliography: gradient_sde.bib
---

The post reviews an AISTATS paper "Scalable Gradients for Stochastic Differential Equations" <d-cite key="gradient_sde"></d-cite>. 

### Neural ODEs

Neural Ordinary Differential Equations (Neural ODEs) are inspired by a model construction like residual networks, recurrent neural network, and based on the following generalization:

$$
h_{t + 1} = h_t + f(h_t, \theta_t) \quad \Rightarrow \quad \frac{dh(t)}{dt} = f(h(t), t; \theta)
$$

By doing so, the discrete layer index in neural network is now understood as continous time index in dynamic systems modeled by an ODE. 

**Adjoint sentivity method for backpropagation** In learning neural network, given an input, we need to forward it by feed to model to produce output. The goal is to compute a gradient w.r.t. $\theta$ so that the parameters will be optimized by gradient descent methods. Computing such a gradient is known as backpropagation, running backward from output through very layer. If there is no discrete layer, how do we backpropagate here? 

In fact, in neural ODEs, at the forward-pass, the output is obtained via a ODE solver which does discretize continuous into smaller time steps. Therefore, we can backpropagate via these intermediate steps. However, it is required to store all of information of these steps to perform normal backward-pass. Avoiding this is one of main contribution of neural ODE. 

Formally, we want to compute the gradient $dL/d\theta$ of 

$$
L(z(t_1)) = L\left(z(t_0) + \int_{t_0}^{t_1} f(z(t); \theta) dt\right) = L(\texttt{ODESolve}(z(t_0), f, t_0, t_1; \theta))
$$

where $L(\cdot)$ is a loss function.

The adjoint sensitivity method compute $$dL/d\theta$ of$ with an extra helping hand of a new guy called *adjoint* $a(t) = \partial L / \partial z(t)$ which agrees with a ODE (similar to chain rule)

$$
\frac{da(t)}{t} = - a(t)^\top \frac{\partial f(z(t), t, \theta)}{\partial z}
$$



Gradient 

$$
\frac{dL}{d\theta} = - \int_{t_1}^{t_0} a(t)^\top \frac{\partial f(z(t), t, \theta)}{\partial \theta} dt
$$

### Neural SDEs

### Stochastic Differential Equations

