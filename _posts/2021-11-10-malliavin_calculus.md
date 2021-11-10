---
layout: distill
title: Mallivian Calculus
description: Some background of Mallivian Calculus
date: 2021-11-10
authors:
  - name: Anh Tong
    url: "https://anh-tong.github.io/"
    affiliations:
      name: KAIST
output: 
  distill::distill_article:
    toc: true
    number_sections: true
    toc_depth: 4
    code_folding: true
  toc_float: 
    collapsed: false
    smooth_scroll: true
---

# Introduction

This is a long post distilling some concepts of Malliavin Calculus and based on the <a href="http://hairer.org/notes/Malliavin.pdf">lecture note</a> of <a href="https://en.wikipedia.org/wiki/Martin_Hairer"> Martin Hairer</a>. 

**Motivation** Malliavin calculus is a modern tool tackling with differentiating random variable defined on a Gaussian probability space w.r.t. the underlying noise.

At the moment, I feel like White Noise Theory and Malliavian calculus share some similarity. They surely complement each other but I do not comprehend the difference between them, for example, what one can do but other cannot.
I also plan to get to know more some background of <a href="http://www.hairer.org/notes/RoughPaths.pdf">rough path</a> but this will be in another post. 

Stochastic analysis centers around stochastic differential equations, i.e.,

$$
dX_t = V_0(X_t)dt + \sum_{i=1}^m V_i(X_t) \circ dW_i(t)
$$

where $\circ dW_t$ denotes Straonovich integration. In this equation, Hairer considers multiple noise parts. 

# White noise and Wiener chaos

This section concerns the definition of white noise under functional representation. Wiener chaos gives the decomposition form of white noise in which we will find somewhat similar to Fourier analysis or <a href="Sobolev space">Sobolev space</a>. 

Now, let's talk about spaces we will work on

- $H = L^2(\mathbb{R}_+, \mathbb{R}^m)$: a real and separatable Hilbert space
- $L^2(\Omega, \mathbb{P})$: for some probability space $(\Omega, \mathbb{P})$

White noise is linear isometry<dt-fn>linear map preserving distance</dt-fn>s $W: H \to L^2(\Omega, \mathbb{P})$ such that the ouput $W(h)$ is a real-valued Gaussian variable or

$$\mathbb{E}[W(h)], \qquad \mathbb{E}[W(h)W(g)] = \langle h, g \rangle_H.$$

The above is just the definition. How to establish such map will be shown next.

**Orthonormal basis** Here, we define 
- a sequence of i.i.d. normal random variable $\{\xi_n\}_{n\geq 0}$
- an orthonormal basis $\{e_n\}_{n \geq 0}$ of $H$. 

When representing $h = \sum_n h_n e_n \in H$, we construct $W(h)=\sum_n h_n \xi_n$. The normal random variable $\xi_n$ is now can rewrite in the functional form form $\xi_n = W(e_n)$.

In the lecture, $m$-dimensional Wiener process is defined by using funtion $\mathbf{1}_{[0,t)}^{(i)}$

$$
(\mathbf{1}_{[0,t)}^{(i)})_j(s) = \begin{cases}
   1 &\text{if } s \in [0, t) \text{ and } j=i \\
   0 &\text{otherwise } 
\end{cases}
$$

Note that 1-dimensional case is easy to show, but for now, still follow the setup in the lecture. 

The $i$-th dimension of Wiener process is defined as $W_i(t) = W(\mathbf{1}_{[0,t)}^{(i)})$ where we can check the covariance 

$$
\mathbb{E}[W_i(t)W_j(s)] = \langle \mathbf{1}_{[0,t)}^{(i)}, \mathbf{1}_{[0,s)}^{(j)} \rangle = \delta_{ij}(t \wedge s).
$$

For arbitrary $h$, $W(h)$ can represent as (Wiener-Ito integral)

$$
W(h) = \sum_{i=1}^m \int_0^\infty h_i(s) dW_i(s)
$$

Note that we may need to clearly differentiate between $W(h)$ and $W_i(s)$. 

**Basis with Hermite polynomials**

There are several formulation of Hermite polynomial

- Recursive $H'_n(x) = n H_{n-1}(x)$
- A different recursive $H_{n + 1}(x) = xH_n(x) - H'_n(x)$, 
- Explicit representation $H_n(x) = \exp\left(-\frac{D^2}{2}\right) x^n$, where $D$ is the differentiation w.r.t. to $x$, $\exp(\cdot)$ is defined in the Taylor expansion sense. 

Some properties of Hermite polynomials:

- $\mathbb{E}[H_n(X)] = 0$: $H_n(X)$ has zero-mean when $X \sim \mathcal{N}(0,1)$
- Identity 

$$
\begin{aligned}
\int H_n(x) H_m(x) e^{-x^2/2} dx  = & 
\frac{1}{n + 1} \int H'_{n + 1}(x) H_m(x) e^{-x^2/2} dx \\
 = & \frac{1}{n + 1} \int H_{n + 1}(x) (xH_m(x) - H'm(x)) e^{-x^2/2} dx \\
 = & \frac{1}{n + 1} \int H_{n + 1}(x) H_{m + 1}(x) e^{-x^2/2} dx
\end{aligned}
$$

This recursive leads to $\mathbb{E}[H_n(X)H_m(X)] = n! \delta_{n.m}$

# The Malliavin derivative and its adjoint

**Goal**: Rigorously define differentation w.r.t. white noise. 

In Wiener process, we usually encounter that its derivative is a Gaussian noise, $\xi_i(t) = \frac{dW_i}{dt}$

The new operator $\mathscr{D}_t^{(i)}$ takes derivative of a random variable w.r.t to $\xi_i(t)$. We may expect this operator works as

$$
\mathscr{D}_t^{(i)} W(h) = h_i(t)
$$

It is because 

$$
W(h) = \sum_{i=1}^m \int_0^\infty h_i(t)\xi_i(t) dt.
$$

We also expect the chain rules


$$
\newcommand\sD{\mathscr{D}}
\sD_t^{(i)} F(X1, \dots, X_n) = \sum_{k=1}^n \partial_k F(X_1, \dots, X_n)\sD_t^{(i)}X_k
$$


A very important tool

$$
\mathbb{E}[\langle \mathscr{D}X, h\rangle] = \mathbb{E}[XW(h)]
$$


# Applications

## Pricing and hedging financial options

## The Black-Scholes model

## Pricing and hedging options in the Black-Scholes model

## Sensibility with respect to the parameters: the greeks
