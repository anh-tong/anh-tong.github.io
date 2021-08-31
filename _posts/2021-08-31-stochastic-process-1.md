---
layout: post
title: Stochastic Processes - Some definitions
date: 2021-08-31 11:12:00
description: Stochastic Process - Some definitions
---
This note contains a self-contained summary of <a href="https://almostsuremath.com/stochastic-calculus">Almostly Sure</a> 


Stochastic process
$$
\begin{aligned}
\mathbb{R}_+ & \to \mathbb{R} \\
t & \mapsto X_t(\omega)
\end{aligned}
$$

Indistinguishable $\mathbb{P}(X_t(\omega)= Y_t(\omega)) = 1 \forall \omega, t$. This also means "almost sure".

Filtration $\{\mathcal{F}_t\}_{t>0}$ is defined to track the set of observable events **up to** time $t$.

Martingale is a stochastic process staying the same on average
$$X_s = \mathbb{E}[X_t| \mathcal{F}_s]$$

