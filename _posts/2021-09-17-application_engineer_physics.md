---
layout: distill
title: Stochastic Calculus in Engineering and Physics 
date: 2021-09-17
description: Summarize some applications of stochastic calculus in engineering and physics. 
---

In this blog, I will summarize several notable applications of stochastic calculus in engineering and physics. Although there are a lot more modern approaches, what will be discussed here is fundamental, still worth understanding in details. The content is based on Chapter 14 of <a href="https://www.worldscientific.com/worldscibooks/10.1142/p821">this book</a>.

As stochastic calculus mostly involves deriving integrations, in engineering applications, we may encounter some situations that we need to utilize such integrations. 

## Filtering

*What is filtering?* Simply speaking, filtering is the process that we *filter out* noise out of a signal.  

Consider a observed process $$Y(t)$$ and its corresponding filtration $$\mathcal{F}_t^Y=\sigma(Y(s), s \leq t)$$. Let's say that there is a (linear) transformation from $$Y(t)$$ to $$X$$.

The goal here is to find an estimate of $$\pi_{X}(t)$$ (probability distribution) such that

$$
\mathbb{E}[(X(t) - Z(t))^2 \mid \mathcal{F}_t] 
$$

where $$Z(t)$$ varies over all $$\mathcal{F}_t$$-measurable processes. In general, we can define an adapted process $$h(t)$$

$$
\pi_t(h) = \mathbb{E}[h(t)| \mathcal{F}_t].
$$

Here, we want to solve a general solution for a non-linear version of $$h(t)$$. 

$$
\begin{align*}
dh(t) = & H(t) dt + dM(t)\\
dY(t) = & A(t) dt + B(Y(t)) dW(t)
\end{align*}
$$
where

+ The process $$M(t)$$ is a $$\mathcal{F}_t$$-martingale
+ The process $$W(t)$$ is a $$\mathcal{F}_t$$-Brownian motion
+ The processes $$H(t)$$, $$A(t)$$ and $$B(t)$$ are "well-defined".

The following theorem gives us a representation of an increment of the estimate $$\pi_t(h)$$

**Theorem** 

$$
d\pi_t(h)= \pi_t(H)dt + (\pi_t(D) + \frac{\pi_t(hA) - \pi_t(h)\pi_t(A)}{B(Y(t))} )d\overline{W}(t)
$$
where $$d\overline{W}(t) = \frac{dY(t) - \pi_t(A)}{B(Y(t))}$$ is an $$\mathcal{F}^Y_t$$-Brownian motion and $$D(t) = \frac{d\langle M, W \rangle (t)}{dt}$$

**Theorem** Let $$A(t)$$ be an $$\mathcal{F}_t$$-adapted process such that $$\int_0^T \mathbb{E}[\lvert A(t) \rvert] dt < \infty$$ and $$V(t) = \int_0^t A(s) ds$$. Then,

$$
\pi_t(V) - \int_0^t \pi_s(A)ds = \mathbb{E}\left[\int_0^t A(s) ds \mid \mathcal{F}_t^Y\right] - \int_0^t\mathbb{E}\left[ A(s) \mid \mathcal{F}_t^Y\right]  ds
$$

is a $$\mathcal{F}_t^Y$$-martingale.

*Remark* As $V(t)$ is a cumulative value of $A(s)$. This theorem is saying that if we exchange $\pi$ and $\int_0^t$, the difference become martingale which mean staying the same on average.


**Theorem** Let $M(t)$ be a $\mathcal{F}_t$ martingale. Then $\pi_t(M)$ is a $\mathcal{F}^Y_t$-martingale.

**Corollary** 

$$
\pi_t(h) = \pi_t(0) + \int_0^t \pi_s(H)ds + M_1(t) + M_2(t) + M_3(t)
$$

where $M_i(t)$ are martingales null at zero:

+ $M_1 = \mathbb{E}[h(X(0))| \mathcal{F}_t^Y] - h(0), $
+ $M_2 = \mathbb{E}\left[\int_0^t H(s) ds| \mathcal{F}_t^Y \right] - \int_0^t \pi_s(H)ds, $
+ $M_3 = \mathbb{E}[M(t)| \mathcal{F}_t^Y], $

## Random Oscillators

Many real-world physical systems are governed by a differential equation

$$
\ddot{x} + h(x, \dot{x}) = 0
$$

Note that the dot over a variable like $$\dot{x}$$ indicates the derivative with respect to the time variable $t$. 

However, the equation is not exactly equal zero but a white noise. Therefore, the stochastic version is under the form

$$
\ddot{X} + h(x, \dot{X}) = \sum_i f_i(X, \dot{X})\dot{W}_i(t)
$$

where $W_i(t)$ are Brownian motions. 

Now, all the results of Ito calculus become handy in this case. In fact, we need to reformulate the problem with $x_1 = x, x_2 = \dot{x}$ and use Ito's lemma 

$$
\begin{align*}
dX_1 =& X_2 dt\\
dX_2 =& \left(-h(X_1,X_2) + \pi \sum_{j,k}K_{ij}f_j(X_1,X_2)\frac{\partial f_k}{\partial x_2}(X_1, X_2)\right)dt + \sum_{i=1}^2 f_i(X_1, X_2)dW_i(t)
\end{align*}
$$

This can be converted into a high-dimensional equation where $$\mathbf{X}(t) = [X_1(t), X_2(t)]^\top$$

The solution for these equations is
$$
\mathbf{X}(t) = \exp(Ft)\left(\mathbf{X}(0) + \int_0^t \exp(-Fs) [0, \sigma]^\top dB(s)\right)
$$




