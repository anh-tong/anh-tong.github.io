---
layout: distill
title: Self-similarity and long-range dependence in fractional Brownian motions
date: 2021-11-03
description: 
---

I came across this <a href="http://www.columbia.edu/~ad3217/fbm/thesis.pdf">thesis</a> and want to take a note on the concepts of self-similarity and long-range dependence which are among notable properties of fractional Brownian motion. Possibly one reason why the term "fractional" is in the name of this stochastic process is that there is a <a href="https://en.wikipedia.org/wiki/Self-similarity">close connection</a> between self-similarity definition and fractals.

## Definition of self-similarity

In a general sense, self-similar object looks exactly or approximately similar to *a part* of itself (which is also mean a small scaled version the object). 

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Fractal_fern_explained.png/300px-Fractal_fern_explained.png">

This image (source: <a href="https://en.wikipedia.org/wiki/Self-similarity">Wikipedia</a>) is a beautiful illustration for self-similarity here.

In statistics, roughly speaking, a stochastic process is self-similar if any finite samples from the process has the same ditribution with a *scaled* version of aggregation (mean, first-order statistic) of the finite samples.

Mathematically, consider a discrete stochastic process $X_k$. For any $m > 1$, a new stochastic process $X^{(m)}_k$ is defined as

$$X^{(m)}_k = \frac{1}{m} (X_{km} + \dots + X_{(k+1)m - 1})$$

If we take a finite sample of $X$ and scaled version of $X^{(m)}$, for example,

$$(X_{k_1}, \dots, X_{k_d}) \quad ,\quad (m^{1-H}X_{k_1}^{(m)}, \dots,m^{1-H}X_{k_d}^{(m)})$$

and these two have the same distribution, we say $X$ is self-similar with Hurst parameter $H$. 

## Definition of long-range dependence

The long-range dependence is decided by autocovariance function $\gamma(k)$. We say a stochastic process has *long-range dependence*, long memory if the sum of autocovariance is unbounded, 

$$
\sum_{k=0}^\infty \gamma(k) = \infty
$$

Still, $\gamma(k)$ decays. 

In most cases, to identify long-range dependence, one may consider the form

$$
\gamma(k) = \mathcal{O}(\lvert k \rvert^{-\alpha})
$$

Note that under long-range dependence, some statistical tests may be affected as the standard deviation of the mean of $X$ is different from the estimation that does not assume long-range dependence, resulting in incorrect confidence intervals in the tests.


## Fractional Brownian motion

Fractional Brownian motion, $B^H$, is an generalization of Browian motion, sharing some properties with Brownian motions such as

1. Stationary increments
2. Start at 0 and having zero mean

Fractional Brownian motion is also viewed as a Gaussian process with covariance

$$
R^H(t, s) = \frac{1}{2}\{t^{2H} + s^{2H} - (t - s)^{2H}\}
$$

The noise corresponding to this is defined as $X$

$$
X_k = B^H(k + 1) - B(ks)
$$

Fraction Brownian *noise* appears to exhibit both long-range dependence and self-similarity.

**Self-similarity** 

Let's compare between $mX^{(m)}$ and $m^HX$. These two have zero mean. The following says that they have the same covariance

$$
\begin{aligned}
& \text{Cov}(X_{km} + \dots, X_{(k+1)m - 1}, X_{lm} + \dots, X_{(l+1)m - 1}) \\
= & \text{Cov}(B^H((k+1)m) - B^H(km), B^H((l+1)m) - B^H(lm)) \\
= & \text{Cov}(m^H(B^H(k+1) - B^H(k)), m^H(B^H(l+1) - B^H(l))) \\
= & \text{Cov}(m^H X_k, m^H X_l)
\end{aligned}
$$

To this point, we can say they have same distribution because they are both Gaussian, having same mean and covariance.


**Long-range dependence**
The autocovariance in this case is

$$\gamma(k) = \frac{1}{2}(\lvert k-1 \rvert^{2H} - 2 \lvert k \rvert^{2H} + \lvert k+1 \rvert^{2H})$$

we can obtain that 

$$\gamma(k) = \mathcal{O}(k^{2H-2})$$

It is because Taylor expansion of $h(x) = (1 - x)^{2H} - 2 + (1 + x)^{2H}$ and $\gamma(k) = \frac{1}{2}k^{2H}h(1/k)$. So $\sum \gamma(k) = \infty$ when $1/2<H< 1.$



