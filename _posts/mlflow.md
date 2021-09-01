---
layout: post
title: Tools keeping track of your experiments
date: # TODO: specify this
description: MLflow
---

### Why

It has been a certain trend recently that MLops has been caught attention from people in industry. 

Unlike software development which has a very mature lifecycle for a project, machine learning projects instrinsically have different characteristics. 
Machine learning models need to keep track of which data they are trained on as well as their internal parameters. Such parameters cannot be differentiated between versions.
Also, we may train our models multiple times when we are at the intial stage of developing the models needing some trials and error, or to select best hyperparmeters. We need to keep track of tasks like this. 
For machine learning at production, it's even more important to know which version is running, whether trained models meet desired requirements.

### When

### What
There are some alternatives or extensions of MLflow in the followings:
1. <a href="https://www.comet.ml/site/"> Comet ML</a>
2. <a > </a>

### How

+ MLflow tracking mode: local, remote
+ What being tracked: Github commit, input arguments, output artifacts
+ Model served


