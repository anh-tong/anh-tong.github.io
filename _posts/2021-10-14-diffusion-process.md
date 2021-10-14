---
layout: distill
title: Diffusion processes
description: Note on diffusion processes
date: 2021-10-14
---

This note focuses on studying diffusion processeses. The setting here is that we are solving stochastic differential equations (SDEs). The name "diffusions" is refered as the solutions to SDEs.

There is a recent direction in generative model (i.e., <a href="https://arxiv.org/abs/2011.13456"> scored-based generative modeling</a>) where the backbone is a diffusion process. Also, <a href="https://anh-tong.github.io/blog/2021/application_machine_learning/">the previous post</a> has discussed the importance of SDEs in Langevin optimization. So let's dive in the main content.

## Martingales and Dynkin's Formula

Let $X(t)$ solve

$$
dX(t) = \mu(X(t), t) dt + \sigma(X(t),t)dB(t), \quad t \geq 0
$$

Define an operator $L_t$ 

$$
L_t f(x,t) = \frac{1}{2}\sigma^2(x,t) \frac{\partial^2 f}{\partial x^2} (x,t) + \mu(x, t) \frac{\partial f}{\partial x}(x,t)
$$

This is simply a shorthand version of <a href="https://en.wikipedia.org/wiki/It%C3%B4%27s_lemma">Ito's formula </a> and we can write

$$
df(X(t),t) = \left(L_tf(X(t),t) + \frac{\partial f}{\partial t}(X(t),t)\right) dt + \frac{\partial f}{\partial x}(X(t), t)\sigma(X(t),t) dB(t)
$$

The first result is presented here is that the following process is a martingale

$$
M_f(t) = f(X(t), t) - \int_0^t \left( L_u + \frac{\partial f}{ \partial t}\right)(X(u), u) du
$$

Of course, $X(t)$ and $f(x, t)$ have to satisfy a "reasonable" condition which will not be written in detail here. 

The above equation totally make sense when we use Ito's lemma and $M_f(t) = \int_0^t \frac{\partial f(B(s), s)}{\partial x} dB(s)$ for the case $X(t) = B(t)$ (Brownian motion). 

Given a function $f(x,t)$ which solves a PDE

$$
L_t f(x, t) + \frac{\partial f}{\partial t}(x, t) =0
$$

and we can say that $f(X(t), t)$ is martingale.

Now, we talk about the expectation. Dynkin's formula will do so, and is obtained straightforward from the martingale property in the previous result. Formally, we have

$$
\mathbb{E}[f(X(t), t)] = f(X(0), 0) + \mathbb{E}\left[\int_0^t \left( L_u + \frac{\partial f}{ \partial t}\right)(X(u), u) du \right]
$$

This is also true if $t$ is replaced by a bounded stopping time $\tau$. 

## Calculation of Expectations and PDEs

This section provide a connection between computing the expectation of diffusion process on the boundary and the corresponding PDEs.

Again, the SDE is written bellow but with a boundary

$$
dX(t) = \mu(X(t), t) dt + \sigma(X(t),t)dB(t),\quad \textcolor{red}{X(s) = x}, \quad t > s \geq 0
$$

One observation here is that the Markov property holds as

$$
\mathbb{E}[g(X(T)) \mid X(t)] = \mathbb{E}[g(X(T))| \mathcal{F}_t]
$$

The following result states the solution of a PDE with boundary is the same with the expectation of the boundary function. Formally, if $f(x, t)$ solve the backward equation, 

$$
L_t f(x, t) + \frac{\partial f}{\partial t}(x, t) =0, \quad \textcolor{red}{f(x,T) = g(x)}
$$

then 

$$
f(x,t) = \mathbb{E}[g(X(T)) \mid X(t)=x]
$$

This result is quite simple to figure out by using the martingale property of $f(x, t)$ as in the previous section. Here is the outline of the proof

$$
\begin{aligned}
\mathbb{E}[f(X(T), T)|\mathcal{F}_t] &= f(X(t), t) \\
\mathbb{E}[g(X(T))|\mathcal{F}_t]&= f(X(t), t)\\
\mathbb{E}[g(X(T))|X(t)]&= f(X(t), t)\\
\mathbb{E}[g(X(T))|X(t)=x]&= f(X(t)=x, t)
\end{aligned}
$$

This result can further extend the case 

$$
L_t f(x, t) + \frac{\partial f}{\partial t}(x, t) = \textcolor{blue}{-\phi(x)}, \quad \textcolor{red}{f(x,T) = g(x)}
$$

then 

$$
f(x,t) = \mathbb{E}\left[g(X(T)) + \int_0^T \phi(X(s))ds \mid X(t)=x \right]
$$

**Feynman-Kac formula** Also, it can even generalize in the following case which is known as Feynman-Kac formula

$$
L_t f(x, t) + \frac{\partial f}{\partial t}(x, t) = \textcolor{blue}{r(x,t)f(x,t)}, \quad \textcolor{red}{f(x,T) = g(x)}
$$

then 

$$
f(x,t) = \mathbb{E}\left[g(X(T))\textcolor{blue}{\exp\left(-\int_t^T r(X(s),s)ds\right)} \mid X(t)=x \right]
$$

*Proof sketch*
From Ito's lemma

$$
\begin{aligned}
df(X(t), t) &= \textcolor{blue}{\left(L_t f(X(t), t) + \frac{\partial f}{\partial t}(X(t), t)\right)}dt + \textcolor{red}{\frac{\partial f}{\partial x}(X(t), t)\sigma(X(t), t) dB(t)} \\
df(X(t), t) & = \textcolor{blue}{r(X(t), t) f(X(t), t)} + \textcolor{red}{dM(t)}
\end{aligned}
$$
Here we used the PDE and defined $M(t)$ in the red term.

This is a linear SDE of Langevin type and its solution is

$$
\begin{aligned}
f(X(T), T) = & f(X(t), t) \exp\left(\int_t^T r(X(u), u) du\right) \\
&+ \exp\left(\int_t^T r(X(u), u) du\right) \int_t^T \exp\left(\int_t^s r(X(u), u) du\right) dM(s) \\
g(X(T)) &= \dots
\end{aligned}
$$
The term associated with $M(t)$ has zero mean is a martingale with zero mean.




<!-- ## Time Homogeneous Diffusions
Now, consider a case of time-independent coefficients SDEs

$$
dX(t) = \mu(X(t))dt + \sigma(X(t))dB(t)
$$ -->


## Remark

The note here does not relate to any part of machine learning research but just is a fundamental background. 

The main takeaway message here is that this problem setting, if we look for expectation, we may need to solve a PDE corresponding to the diffusion process.


