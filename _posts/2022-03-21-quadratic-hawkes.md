---
layout: distill
title: Hawkes processes and Applications in Finance
description: Summarize a line of work in quantitative finance including scale limits of Hawkes processes and quadratic Hawkes processes
date: 2022-03-21
---

Last month, as an attempt to expand my knowledge in a broader area, specifically, mathematical finance for this time, I attended <a href="https://www.centre-cournot.org/conferences_en.html#conference27">this conference</a> focusing on microstructures and macrostructures in markets, how mathematical tools can makes sense of micro-behaviors to obtains macro-properties. The take-away message here is that, at micro levels, financial activities like buying/selling events are better to be modeled by jump processes, especially Hawkes processes which possess some characteristics like self-exciting (i.e., buying leads to more buying). And when talking limit in a mathematical sense, models will converge to some standard models associated to Brownian motions that is well-known in understanding financial models at macro levels.

I try to catch up with literatures and explain the most simple ideas in this post.

### Scale limit of Hawkes processes is Brownian motion

Consider two point processes, $N_1(t)$ and $N_2(t)$ having the same intensity $\mu$. The different between these processes

$$X(t) = N_1(t) -N_2(t)$$

turns out to have an interesting property that when applying a scale $T$ and letting this scale going to infinity, we get a Brownian motion with a scale factor

$$
\lim_{T\to+\infty} \frac{1}{\sqrt{T}}X(tT) = \sqrt{2\mu}B(t), \quad t \in [0,1]
$$

I made a little <a href="https://github.com/anh-tong/scale-limit-hawkes/blob/main/main.ipynb">notebook</a> to verify this empirically. But this can be analytically justified by following the definitition of Brownian motion as we observe the increment $X(t_1T) - X(t_2T)= N_1(t_1T) - N_1(t_2T) - (N_2(t_1T) -N_2(t_2T))$. The interval $[t_1T, t_2T]$ is partitioned into $T$ smaller internal and each of them has $t_1-t_2$. In fact, we have

$$N_1(t_1T) - N_1(t_2T) = \sum_{k=1}^T \texttt{Poisson}(\mu (t_1-t_2))$$

By the central limit theorem, $\frac{1}{\sqrt{T}} \sum_{k=1}^T \texttt{Poisson}(\mu (t_1-t_2)) \to \mathcal{N}(\mu (t_1-t_2), \mu (t_1-t_2))$. Now, at the limit, the difference of two independent normal distributions yields a normal ditribution $\mathcal{N}(0, 2\mu (t_1-t_2))$. This conincides with the increment coresponding to $\sqrt{2\mu}B(t)$. 

### Quadratic Hawkes proceses

Simply, Hawkes process is a point process where we have a specific way of modeling it's intensity function. <a href="https://arxiv.org/abs/1509.07710">This paper </a> proposes quadratic Hawkes processes (QHawkes) - a generalization of Hawkes processes which is able to capture well characteristics in financial time series. The main motivation is that existing work ,i.e., multifractional Brownian motions in stochastic volatility models or FIGARCH, does not provide properties that math with *stylized facts*. Here, the stylized facts are a collective facts observed by empirical analyses. They include, for examples, fat tails of return distributions, slow decay of correlations. More importantly, this paper shows that QHawkes can describe the time reversal asymetry. This is interpreted some think like financial time series are not statistical symmetrical when the past and future are change. This attributes to leverage effect (past returns affects future volatities but not the other way arround).

#### Model description

A QHawkes process is specified by an intensity function as

$$\lambda_t = \lambda_\infty + \frac{1}{\psi} \int_{-\infty}^t L(t-s) dP_s + \frac{1}{\psi^2}K(t-s, t-u) dP_sdP_u$$

Here, $P_t$ is the price at time $t$. $L$ is a leverage kernel. $K$ is a quadratic feedback kernel. In many cases, $L$ is considered to be $0$ and only quadratic kernel is left. When the kernel is diagonal, 
$K(t,s) = \phi(t)\delta_{t-s}$, the model falls back to Hawkes processes. 

For general quadratic kernels, it may not be convienent to have a nice analysis. Instead, by imposing a certain structure and this case is to have "low-rank" form where

$$K(t,s) = \phi(t)\delta_{t-s} + k(t)k(s)$$

is divided into two parts. This leads to a new representation of the intensity function

$$\lambda_t = \lambda_\infty + H_t + Z_t^2$$

with a new interpretations

+ Hawkes terms:
$$H_t := \int_{-\infty}^t \phi(t-s) dN_s, \quad N_t - N_{t^-} = \frac{1}{\psi} (P_t - P_{t^-})^2$$
+ Zumbach term:
$$Z_t := \frac{1}{\psi}\int_{-\infty}^t k(t-s) dP_s$$


#### Time stationary

This notion is equivalent when $\mathbb{E}[\lambda_t]$ is constant, positive and finite. To analyze this properties, the intensity function of QHawkes is written into diagonal terms and off-diagional term:

$$\lambda_t = \lambda_\infty + \mathcal{L}_t + H_t + 2M_t$$

Note that the expectation of $\mathcal{L}_t$ and $H_t$ is zero since we may assume $P_t$ to be a martingale. 

The remain is the off-diagonal term where $$M_t = \frac{1}{\psi^2} \int_{-\infty}^t\Theta_{t,u}  dP_{u}$$ with  $\Theta_{t, u} = \int_{-\infty}^{u-} K(t-u, t-r) dP_{r}$.

Finally, the expectation of intensity is

$$\mathbb{E}[\lambda_t] = \lambda_\infty + \int_{-\infty}^t K(t-s, t-s) \mathbb{E}[\lambda_s] ds.$$
The necessary condition of time stationary (time index does not matter for the expectation of intensity) is obtained as

$$\bar{\lambda} = \frac{\lambda_\infty}{1 - Tr(K)}$$

with 

1. $\lambda_\infty > 0$ and $Tr(K) < 1$
2. $\lambda_\infty = 0$ and $Tr(K) = 1$

#### Auto-correlation

Consider two types of correlation functions: two-points correlation and three-points correlations

$$\mathcal{C}(\tau) = \mathbb{E}\left[\frac{dN_t}{dt}\frac{dN_{t-\tau}}{dt}\right] -\bar{\lambda}^2= \mathbb{E}\left[\lambda_t\frac{dN_{t-\tau}}{dt}\right] -\bar{\lambda}^2$$

$$\mathcal{D}(\tau_1, \tau_2) = \frac{1}{\psi^2}\mathbb{E}\left[\frac{dN_t}{dt}\frac{dP_{t-\tau_1}}{dt}\frac{dP_{t-\tau_2}}{dt}\right]$$

In fact, we can write these two functions in terms of the kernel $K(t,s)$ but they are difficult to solve in general. We may be interested in the asymptotic behaviors of the auto-correlation functions. Note that here the analysis involves only power law decays, how the power coefficients of kernels affect the power coefficients of $\mathcal{C, D}$.

#### Volatility model of ZHawkes

Choosing $k(t) = \sqrt{2n_Z \omega}\exp(-\omega t)$ and $\phi(t)=n_H\beta\exp(-\beta t)$, a ZHawkes process is decomposed into two terms represented as stochastic differential equations:

$$
\begin{aligned}
dH_t &= \beta [-H_t dt + n_H dN_t]\\
dN_t & = -\omega Z_t dt + k_0 dP_t
\end{aligned}
$$

Next, the paper moves to study low-frequency asymptotics to demonstrate the fat-tail behaviors which does not hold in previous work. The technique here again is the *scale limit* like the previous section. 

Let $\bar{H}_t^T = H_{tT}, \bar{Z}_t^T = Z_{tT}, \bar{N}_t^T = N_{tT}$ and $\bar{P}_t^T = P_{tT}$. With the change of variable, the above SDE system becomes

$$
\begin{aligned}
d\bar{H}_t^T &= \beta_T [-\bar{H}_t^T Tdt + n_H d\bar{N}_t]\\
d\bar{N}_t^T & = -\omega_T \bar{Z}_t^T Tdt + \sqrt{2\omega_T n_Z} d\bar{P}_t^T
\end{aligned}
$$

Here $\bar{N}^T$ and $\bar{P}^T$ have the same scaled intensity, $T[\lambda_\infty + \bar{H}_t^T + (\bar{Z}_t^T)^2]$, the 

The infinitesimal generator (see <a href="https://en.wikipedia.org/wiki/Infinitesimal_generator_(stochastic_processes)">wiki</a>) of this ($\gamma_T^2 = 2\omega_T n_Z$)

$$
\begin{aligned}
\mathcal{A}^T f(h,z) = &- \beta_T h T \partial_h f(h,z) - \omega_T z \partial_z f(h,z) \\
&+ T[\lambda_\infty + h + z^2]\left\{\frac{1}{2}f(h + n_H\beta_T, z + \gamma_T) + \frac{1}{2}f(h + n_H\beta_T, z - \gamma_T) - f(h,z) \right\}
\end{aligned}
$$

Rescaling $\beta_T = \bar{\beta}/T, \omega_T=\bar{\omega}/T$, and sending $T$ to infinity yields

$$
\frac{1}{2}f(h + n_H\beta_T, z + \gamma_T) + \frac{1}{2}f(h + n_H\beta_T, z - \gamma_T) - f(h,z) = \frac{n_H \bar{\beta}}{T}\partial_h f(h, z) + \frac{\bar{\gamma}^2}{2T}\partial^2_{zz}f(h,z) + o(\frac{1}{T})
$$

Therefore, the infinitesimal generator and SDE at the limit are

$$
\mathcal{A}^\infty f(h, z) = -\bar{\beta}[(1 - n_H)h - n_H(\lambda_\infty + z^2)]\partial_h f(h, z) - \bar{\omega} z \partial_z f(h,z) + n_Z\bar{\omega}[\lambda_\infty + h + z^2]\partial^2_{zz} f(h, z)
$$

and

$$
\begin{aligned}
d\bar{H}_t^\infty &= \bar{\beta}[-(1 - n_N)\bar{H}_t^\infty + n_H(\lambda_\infty + (\bar{Z}_t^\infty)^2)]dt\\
d\bar{N}_t^\infty & = -\omega_T \bar{Z}_t^\infty Tdt + \bar{\gamma}\sqrt{\lambda_\infty + \bar{H}_t^\infty + (\bar{Z}_t^\infty)^2}dW_t
\end{aligned}
$$

From this SDE, it will be complicated to get fat-tail as it follows some existing work. The key procedure next is to solve the above continuous (not jump) SDE (mostly the first equation) and point out the volatitliy, and it distribution. 

