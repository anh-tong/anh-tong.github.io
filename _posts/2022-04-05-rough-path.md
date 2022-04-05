---
layout: distill
title: Signature and Log Signature in rough path theory
description: Quick review of the central quantities in rough path theory
date: 2022-04-05
bibliography: 2022-04-05-rough-path.bib
---

I have some time to read some basic concepts in rough path theory <d-cite key="Lyons2014"></d-cite>. 

Simple speaking, signature or log signature can capture the characteristic of rough path. This is similar when we think about learning representations of images using convolutional neural networks (CNNs). Both (log) signatures and CNNs do extracts informations but focus on different objects (sequencing data vs image data). 

$$
y_{J_+} = \left(\sum_{n=0}^\infty A^n \iint_{u_1 \leq \dots \leq u_n} d\gamma_{u_1} \otimes \dots \otimes d\gamma_{u_n}\right)y_0
$$

This equation looks intimidating but simply we can understand as solving differential equation iteratively starting from $u_1$ to $u_2$ (solution is $\int Ay_t d\gamma_{u_1} $). The solution on $[u_1, u_2]$ will be the initial conditional to solve differential equation on the next interval $[u_2, u_3]$. 

Inspired by the solution of linear controlled differential equations, the signature is defined as the integral part 

$$
\boxed{
    S(\gamma) := \sum_{n=0}^\infty \iint_{u_1 \leq \dots \leq u_n} d\gamma_{u_1} \otimes \dots \otimes d\gamma_{u_n} \quad \in  \bigoplus_{n=0}^\infty E^{\otimes n}
}$$

### How to compute signature in practice

Here, time series data is the main focus as it is one of the promiment use cases of signatures. 

As noted in <d-cite key="Lyons2014"></d-cite>, the series of signatures converges very fast ( the power of variation over factorial of $n$). Therefore, truncated series carries enough information of a path.

There are softwares already implemented efficiently how to compute (log) signatures from data <d-cite key="kidger2021signatory"></d-cite>. This post will try to demonstrate a simple example. 


Algebra structure defined by $T((\mathbb{R}^d)) = \prod_{k=0}^\infty (\mathbb{R}^d)^{\otimes k}$. (An example for this is $(\mathbb{R}^d)^{\otimes 3}  = \mathbb{R}^d \otimes \mathbb{R}^d \otimes \mathbb{R}^d$ is a tensor shape $(d, d, d)$). 

The product between tensors is denoted as $\otimes$ between $(a_1, a_2, \dots, a_m)$ and $(b_1, b_2, \dots, b_m)$ resulted in $(a_1, \dots, a_n, b_1, \dots, b_m)$. 

An product (denoted as $\otimes$ and let's not be confused with the notation) between $A = (A_0, A_1, \dots)$ and $B=(B_0, B_1, \dots)$ is defined as

$$A \otimes B = \left(\sum_{j=0}^k A_j \otimes B_{k-j}\right)_{k\geq 0}$$

**Stop and breath** Okay! This is also complicated. Maybe just think this an infinite many tensor $d \times d \times \dots $. The product should satisfy a closure property which its ouput should have size $d \times d \times \dots $

**Proposition** (Chen's identity) Roughly speaking, concatenating two paths will result in signature as

$$\text{Sig}(X * Y) = \text{Sig}(X) \otimes \text{Sig}(Y)$$

Now, we can construct signature for stream data by Chen's identity. Let $\mathbf{x} = (x_1, x_2, \dots, x_n)$. Probably the main assumption here is that the path is contructed by straight lines sequentially.

$$
\text{Sig}(\mathbf{x}) = \exp(x_2 - x_1) \otimes \exp(x_3-x_2) \otimes \dots \otimes \exp(x_n - x_{n-1})
$$

here $\exp(\cdot)$ is NOT the exponential function on real set but is defined with operator $\otimes$

$$
\exp(x) = \left(1, x, \frac{x \otimes x}{2!}, \frac{x \otimes x \otimes x}{3!}, \dots\right)
$$

which is an infinite-dimensional vector where components have increasing power orders.




