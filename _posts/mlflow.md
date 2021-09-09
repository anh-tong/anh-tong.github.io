---
layout: dist
title: Tools keeping track of your experiments
date: # TODO: specify this
description: MLflow
---

### Why

It has been a certain trend recently that MLOps has been caught attention from people in industry. 

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

#### Mlflow tracking

Log what you need to log. 

Paramters, metrics, images,  artifacts (any type of data files)

{% highlight python %}
import mlflow

mlflow.log_param() 
mlflow.log_metric()

mlflow.log_artifact()  

{% endhighlight %}

Allow to centralize a server endpoint to manage all running experiments.

We can further retrieve results and refine them. 

{% highlight python %}
from mlflow.tracking import MLflowClient

client = MLflowClient()

{% endhighlight %}


#### Mlflow project

Mlflow project lets us define a set of different tasks. This specifies a environment the code will run on. There are two types: conda environment and docker environment. We may need to configure each of them accordingly. Mlflow project defines multiple entrypoints which are the running script (either ``.py`` or ``.sh``) with parameters. 

{% highlight python %}
import mlflow

current_run = mlflow.run(".", entry_point, parameters)

{% endhightlight %}

I bring an example implemetation of <a> the Automatic Statistician</a> designed using Mflow here. 

**Mlflow project file**

{% highlight %}

{% endhighlight %}

**An entry point performing kernel search**

{% highlight %}

{% endhighlight %}

**A workflow code putting all entry points together**

{% hightlight %}

{% endhighlight %}

Let's say we have a task is to produce a report as a website from all results. In the web server, we can call ``MlflowClient`` to access to any specific run id and retrieve the desired output from model.  


