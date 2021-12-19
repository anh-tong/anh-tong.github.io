---
layout: distill
title: Changepoint detection
date: 
description: Two methods of changepoint detection
---

Changepoint detection is a problem often encountered in sistuations like the abrupt change of systems. It's commonly considered in dynamical system where we need to detect the change. This problem is unarguably important since 

In this post, I will review two approaches on changepoint detection. The first is a Bayesian approach, the second is based on filtering theory connecting to stochastic differential equation.

### Bayesian Online Changepoint Detection

Let's start with [this prominent paper](https://arxiv.org/pdf/0710.3742.pdf). The main assumption of this paper is that given a data, there is a true partition in which .

The method of the paper focuses on the "run length" quantity which keeps track of whether the value at the current time is still staying the same distribution of the current partition.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <img class="center" src="{{ site.baseurl }}/assets/img/BOCPD.png">
    </div>
</div>
<div class="caption">
    The data contains 3 partitions. The below figure explains the run length keep increasing when we stay in the same partition
</div>

**Notation**