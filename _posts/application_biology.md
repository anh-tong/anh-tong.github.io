---
layout: distill
title: Applications in Biology
date: 
description: Introduce some applications of stochastic models including diffusion models, Markove Jump processs, 
---

## Feller's Braching Diffusion

The model centers around a stochastic differential equation

$$
dX(t) = \alpha X(t) dt + \sigma \sqrt{X(t)} dB(t)
$$

This equation can lead to following observations: (1) the population grows exponentially. 

## Wright-Fisher Diffusion


Let say we have two types, $A$ and $a$ in a fixed size population ($N$ is the size). 

When mutations happens, there are two possibilities:  (1) $A$ to $a$, or (2) $a$ to $A$. They have the mutatuation rate $\gamma_1/N$ and $\gamma_2/N$ respectively.

The following equation is trying to model the frequency of type $A$, denoted as $X(t)$:

$$
dX(t) = (-\gamma_1 X(t) + \gamma_2 (1- X(t))) dt + \sqrt{X(t) (1 - X(t))}dB(t)
$$

*Plain-word description*: The change in frequency (left-hand side) has a certain drift which is the total change between two types, and randomness having a certain scale .I'm not sure how it chooses $\sqrt{X(t)(1-X(t))}$ but probably it comes from the lower bound $X(t) + (1 - X(t)) \geq 2\sqrt{X(t)(1-X(t))}$.

There are three scenarios:

+ No mutation at all ($\gamma_1=\gamma_2=0$): There is a fixation (convergence) to either $0$ or $1$ for $X(t)$. 
+ One-way mutation: This is when one of $\gamma_1$ and $\gamma_2$ equals to $0$
+ Two-way mutation: The solution is obtained using diffusion process technique, and is written down as
$$

\pi(x) = \frac{C}{\sigma^2(x)} \exp\left(\int_{x_0}^x \frac{2\mu(y)}{\sigma^2(y)} dy\right) = C(1-x)^{2\gamma_1-1} x^{2\gamma_2 -1}

$$
The key characteristic of this case is that there is no fixation occured but the frequency follows a stationary distribution which is written above as Beta distribution.

## Birth-death process

## Branching process

## Stochastic Lotka-Volerra Model