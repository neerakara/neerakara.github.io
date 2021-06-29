---
title: 'Gaussian Processes for Out-Of-Distribution Detection'
date: 2021-06-30
permalink: /notes/gps-ood/
tags:
  - gaussian processes
  - out-of-distribution detection
---

### Gaussian processes (GPs)
([Rasmussen 2003](https://link.springer.com/content/pdf/10.1007%2F978-3-540-28650-9_4.pdf), [Rasmussen, Williams 2006](http://www.gaussianprocess.org/gpml/chapters/RW.pdf), [Görtler, Kehlbeck, Deussen | Konstanz | Distill 2019](https://distill.pub/2019/visual-exploration-gaussian-processes/))

 A random process / stochastic process is a sequence of random variables $X_1, X_2, ..., X_T$.
 A random field / stochastic field is when the random variables of interest occur in 2 or more dimensions (eg $X_{ij}, i=1, 2..N, j=1,2,..M$).
 We define a particular family of random processes / fields (e.g. Bernoulli process, Markov process, Markov random fields, Gaussian processes, etc.)
 by choosing a family of distributions to represent the joint PDF over the random variables in question.
 For instance, a stochastic process is called a GP if the joint distribution over the RVs $X_1, X_2, ..., X_T$ is a multivariate gaussian distribution.
 If the sequence of RVs is defined over a continuous domain, we have a joint distribution over infinitely-many RVs -
 in other words we have a distribution over functions in a continuous domain. Multivariate gaussian distributions are defined by a mean vector and a covariance matrix.
 Accordingly, gaussian processes are defined by a mean function $m(x)$ and a covariance function $k(x_i, x_j)$.
 We write $f \sim GP(m, k)$ and say 'the function $f$ is distributed as a GP with mean function $m$ and covariance function $k$'.
 If the covariance function depends only on the distance between $x_i$ and $x_j$, and not on their absolute values, the gaussian process is said to be $\textit{stationary}$.

 GPs can be used in several ways:
  * As priors over functions, with the covariance function that defines the GP representing the smoothness of the prior -->
  $f(x_i)$ and $f(x_j)$ are correlated according to the distance between $x_i$ and $x_j$, and the smoothness defined by the covariance function $k(x_i, x_j)$.
  * Updating the prior in the light of training data - in other words, computing the posterior GP.
  Consider a scenario where we know the value of a function at a number of training input points $x_i, i=1, .. n$,
  and are interested in knowing the distribution over the function values at a number of test input points $x_j^{test}, j=1, .. m$.
  According to the GP, the joint distribution of the vector ($\in \mathcal{R}^{m+n}$) of function values of all training as well as test points
  is a multivariate gaussian distribution (defined by a mean vector and a covariance matrix).
  The conditional distribution of the function values at the test points given the function values at the training points is also
  a gaussian distribution whose parameters can be computed analytically in terms of the training data and the covariance function.
  A computational concern is that the mean vector and the covariance matrix of the posterior GP depend on the inverse of the covariance matrix of the training datapoints.
  This inversion is $O(n^3)$.
  * Training the GP prior: This refers to specifying a GP's mean and covariance function upto some parameters
  and then finding maximum likelihood estimates for these parameters using available data.

### Sparse GPs
([Snelson, Ghahramani | UCL | NeurIPS 2005](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.60.2209&rep=rep1&type=pdf), [Hensman, Fusi, Lawrence | Sheffield 2013](https://arxiv.org/ftp/arxiv/papers/1309/1309.6835.pdf))

SGPs introduce $m$ ($<< n$) new input points (called psuedo-inputs or $\textit{inducing points}$),
such that the distribution of the function values at test points conditioned on the new data points is close to the one conditioned on the original $n$ data points,
with the computational benefit that one has to now invert only a $m$x$m$ covariance matrix instead of a $n$x$n$ one.
    

### Deep GPs
([Damianou, Lawrence | Sheffield | AISTATS 2013](http://proceedings.mlr.press/v31/damianou13a.pdf))

### Convolutional GPs
[Wilk, Rasmussen, Hensman | Cambridge | NeurIPS 2017](https://arxiv.org/pdf/1709.01894.pdf))

### Deep convolutional GP
([Blomqvist, Kaski, Heinonen | Helsinki 2019](https://arxiv.org/pdf/1810.03052.pdf))

### Distributional GPs
[Popescu, Sharp, Cole, Glocker | Imperial College London | 2020](https://arxiv.org/pdf/2010.14877.pdf))

### Distributional Gaussian Process Layers for Outlier Detection in Image Segmentation
([Popescu, Sharp, Cole, Kamnitsas, Glocker | Imperial College London | IPMI 2021](https://link.springer.com/content/pdf/10.1007%2F978-3-030-78191-0_32.pdf))
