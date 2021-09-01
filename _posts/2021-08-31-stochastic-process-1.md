---
layout: post
title: Stochastic Processes - Some definitions
date: 2021-08-31 11:12:00
description: Stochastic Process - Some definitions
---
This note contains a self-contained summary of <a href="https://almostsuremath.com/stochastic-calculus"> Almost Sure</a> 

##### Definition
Stochastic process

$$
\begin{align*}
\mathbb{R}_+ & \to \mathbb{R} \\
t & \mapsto X_t(\omega)
\end{align*}
$$

Indistinguishable $$\mathbb{P}(X_t(\omega)= Y_t(\omega)) = 1 \quad \forall \omega, t$$. This also means "almost sure".

##### Filtration
**Filtration** $$\{\mathcal{F}_t\}_{t>0}$$ is defined to track the set of observable events **up to** time $$t$$.

A stochastic process $$X$$ is *adapted* if $$X_t$$ is an $$F_t$$-measurable random variable from each time $$t \geq 0$$. 

**Martingale** is a stochastic process staying the same on average
\begin{equation}
X_s = \mathbb{E}[X_t \mid \mathcal{F}_s]. \notag
\end{equation}

**Submartingale** if integrable and $$X_s \leq \mathbb{E} [X_t \mid {\mathcal{F}_s} ]$$

**Supermartingale** if integrable and $$X_s \geq \mathbb{E} [X_t \mid {\mathcal{F}_s}]$$

#### Elemetary integrals
Martingales and submartingales are well-behaved under stochastic integration. 

**Elemetery process** is defined as
$$
    \xi_t = Z_0 1_{\{t=0\}} + \sum_{k=1}^n Z_k 1_{\{s_k < t \leq t_k\}}. 
$$

Stochastic integrals of such elementary process is


$$
    \int_0^\infty \xi dX = \sum_{k=1}^n Z_k(X_{t_k} - X_{s_k})
$$

**Theorem**
An adapted integrable process $$X$$ is 
+ a martingale iff
  \begin{equation}
    \mathbb{E}\left[\int_0^\infty \xi dX \right] = 0 \notag
  \end{equation}
for all bounded elementary processes $$\xi$$.
+ a submartingale iff
  \begin{equation}
    \mathbb{E}\left[\int_0^\infty \xi dX \right] \geq 0 \notag
  \end{equation}
for all  bounded elementary process $$\xi$$


**Proof**
Prove the second one. Suppose $$X$$ is submartingale.

\begin{equation}
    \mathbb{E}\left[\int_0^\infty \xi dX\right] = \sum_{k=1}^n \mathbb{E}[Z_k(X_{t_k} - X_{s_k})]
 = \sum_{k=1}^n \mathbb{E}[Z_k(\mathbb{E}[X_{t_k} \mid \mathcal{F}_{s_k}] - X_{s})] \geq 0
\end{equation}

Conversely, choose any $$s < t \in \mathbb{R}_+$$, define a process $$\xi_u = 1_A 1_{\{s <u \leq t\}}$$ where $$A \in \mathcal{F}_s$$ and
\begin{equation}
    \mathbb{E}[1_A(X_t-X_s)]= \mathbb{E}\left[\int_0^\infty \xi dX\right] \geq 0
\end{equation}
Choose $$A = \{\mathbb{E}[X_t \mid \mathcal{F}_s] \leq X_s\}$$, 

\begin{equation}
0 \geq \mathbb{E}[\min(\mathbb{E}[X_t \mid \mathcal{F}_s] - X_s, 0)] = \mathbb{E}[1_A(X_t - X_s) ] \geq 0
\end{equation}

Any non-positive random variable whose expectation is zero must be equal to zero, almost surely. Therefore, $$E[X_t \mid \mathcal{F}_s] \geq X_s$$