---
layout: distill
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

A stochastic process $$X$$ is *adapted* if $$X_t$$ is an $$\mathcal{F}_t$$-measurable random variable from each time $$t \geq 0$$. 

**Martingale** is a stochastic process staying the same on average
\begin{equation}
X_s = \mathbb{E}[X_t \mid \mathcal{F}_s]. \notag
\end{equation}

**Submartingale** if integrable and $$X_s \leq \mathbb{E} [X_t \mid {\mathcal{F}_s} ]$$

**Supermartingale** if integrable and $$X_s \geq \mathbb{E} [X_t \mid {\mathcal{F}_s}]$$

#### Stopping times
A stopping time is a random time which is adapted to the underlying filtration. Formally, A stopping time is a map $$\tau: \Omega \to \mathbb{R}_+ \cap \{\infty\}$$ such that the event $$\{\tau \leq t\} \in \mathcal{F}_t$$ for each $$t \geq 0$$. 

**Theorem (Debut theorem)** Let $$X$$ be an adapted right-continuous stochastic process defined on a complete filtered probability space. 

$$
  \tau(\omega) = \inf \{t \in \mathbb{R}_+: X_t(\omega) \geq K\}
$$

is a stopping time. 

A process $$X$$ stopped at the random time $$\tau$$ is denoted by $$X^\tau$$

$$
  X^\tau_t(\omega) = X_{t \wedge \tau (\omega)}(\omega).
$$



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

$$
    \mathbb{E}\left[\int_0^\infty \xi dX\right] = \sum_{k=1}^n \mathbb{E}[Z_k(X_{t_k} - X_{s_k})]
 = \sum_{k=1}^n \mathbb{E}[Z_k(\mathbb{E}[X_{t_k} \mid \mathcal{F}_{s_k}] - X_{s})] \geq 0
$$

Conversely, choose any $$s < t \in \mathbb{R}_+$$, define a process $$\xi_u = 1_A 1_{\{s <u \leq t\}}$$ where $$A \in \mathcal{F}_s$$ and
\begin{equation}
    \mathbb{E}[1_A(X_t-X_s)]= \mathbb{E}\left[\int_0^\infty \xi dX\right] \geq 0
\end{equation}
Choose $$A = \{\mathbb{E}[X_t \mid \mathcal{F}_s] \leq X_s\}$$, 

\begin{equation}
0 \geq \mathbb{E}[\min(\mathbb{E}[X_t \mid \mathcal{F}_s] - X_s, 0)] = \mathbb{E}[1_A(X_t - X_s) ] \geq 0
\end{equation}

Any non-positive random variable whose expectation is zero must be equal to zero, almost surely. Therefore, $$E[X_t \mid \mathcal{F}_s] \geq X_s$$

#### Upcrossings, Downcrossings, and Martingale Convergence

The number of times that a process passes upwards and downwards through an interval. 

A sequence converges iff the number of upcrossings is finite for all intervals.

**Lemma (Doob's upcrossing lemma)** Let $$X_t$$ be a supermartingales with time $$t$$ in a countable index set, the number of upcrossings $$(b- a) \mathbb{E}[U[a, b]]\leq \sup_t \mathbb{E}[(a - X_t) \vee 0]$$

**Theorem (Doob's Forward Convergence Theorem)** If martingale and the expected absolute value is bounded, then the process converges with prob. $$1$$. 

*Proof*. Use the previous lemma, and <a href="https://en.wikipedia.org/wiki/Fatou's_lemma#Standard_statement_of_Fatou.27s_lemma"> Fatou's lemma </a>. 

**Theorem (Levy's upward theorem)** With $$\{\mathcal{F}_n\}_{n \in \mathbb{N}}$$ and $$\mathcal{F}_\infty=\sigma(\cup_n \mathcal{F}_n)$$. For any integral random variable $$X$$, $$\mathbb{E}[X \mid \mathcal{F}_n] \to \mathbb{E}[X \mid \mathcal{F}_\infty]$$, with a prob. $$1$$.

**Theorem (Levy's downward theorem)** Similar to the above result but $$\mathcal{F}_\infty=\sigma(\cap_n \mathcal{F}_n)$$

**The Strong Law of Large Numbers** 
The sample mean of i.i.d. random variables converges to the mean with the prob. one. 

It is easy to use the above result to prove this (while challenging with elementary probability). 

Let $$S_n = X_1 + X_2 + \dots + X_n$$, define $$\mathcal{F}_n = \sigma(S_n, S_{n+1}, \dots)$$, then
$$\mathbb{E}[X_1 \mid \mathcal{F}_n]=\mathbb{E}[X_2 \mid \mathcal{F}_n]=\dots = \mathbb{E}[X_n \mid \mathcal{F}_n]$$

$$\mathbb{E}[X_1 \mid \mathcal{F}_n] = \frac{1}{n}\left(\mathbb{E}[X_1 \mid \mathcal{F}_n]+\mathbb{E}[X_2 \mid \mathcal{F}_n]+\dots + \mathbb{E}[X_n \mid \mathcal{F}_n]\right) = \frac{S_n}{n}$$
By Levy's downward theorem, $$\frac{S_n}{n}=\mathbb{E}[X_1 \mid \mathcal{F}_n] \to \mathbb{E}[X_1 \mid \mathcal{F}_\infty]$$

#### Cadlag Modifications
Motivation:

+ Choose good versions of stochastic processes
+ The following result guarantees that many of stochastic process have a right-contiuous version and have left limits everywhere. (Right Continuous and Left Limits)

These processes are called *càdlàg* or cadlag. 

**Theorem** Let $$X$$ be an adapted stochastic process and either

+ $$X$$ 
is integrable and
$$\mathbb{E}\left[\int_0^t 1_AdX\right]$$ 
is bounded with $$A$$
is elementary

+ $$\int_0^t 1_AdX$$
is bounded in probability.

Then it has a cadlag version.

**Theorem** Let $$X$$ be a martingale which is right-continuous in probability. Then, it has a cadlag version.

**Theorem** Let $$\{X_t\}_{t \in \mathbb{T}}$$ be a submartingale w.r.t. a filtered probability space. Then $$X_{t_n}$$ is uniformly integrable for any sequence $$t_n$$ bounded bellow in $$\mathbb{T}$$.