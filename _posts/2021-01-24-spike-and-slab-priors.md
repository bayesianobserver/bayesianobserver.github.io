---
layout: post
title: "Spike and Slab priors"
date: 2021-01-24
mathjax: true
---

In variable selection problems where the number of predictors is large relative to the number of data points, the optimization of penalized objective functions represents a convenient approach to regularization. The $L_2$-penalty (ridge regression), and $L_1$-penalty (Lasso regression) are most common. There is even a penalized regression called elasticnet regression, that combines the $L_1$ and $L_2$ penalties as a convex sum. Looked at from a Bayesian lens, the $L_2$-penalized regression solution is the mode of the posterior distribution if a Gaussian prior is placed on each of the linear regression coefficients, while the Lasso solution is the mode of the posterior if a Laplacian distribution is used as the prior instead. The Laplacian distribution, being non-differentiable at 0, is peakier than the Gaussian distribution, and as a result it results in a sparse solution.

<p align="center">
  <img width="320"  src="/assets/spikeslab.png">
</p>

The Lasso or $L_1$-penalty is really a relaxation to the original problem of variable selection, which requires a $L_0$-penalty (the $L_0$ norm of the coefficient vector is the number of non-zero coefficients). However, appending the $L_0$ norm to the standard linear regression objective function destroys the convexity of the optimization problem. The $L_1$-norm is the smallest norm that preserves convexity in the penalized objective function, while serving as a convenient relaxation to the $L_0$ norm.

A spike-and-slab distribution is a mixture of two Gaussians, one that is very peaky (i.e. low variance - this is the spike) and another that is very broad (i.e. high variance - this is the slab).

With a spike of zero variance (a Dirac Delta function), the spike and slab prior perfectly expresses the original variable selection criterion of either accepting or rejecting a variable. However, with this prior, there is no closed form penalty function that can simply be appended to the original objective function and the result minimized. The formulation requires the computation of a full posterior distribution and in the absence of a convenient conjugacy relationship, the only way out is to do MCMC sampling (another approach might be variational inference, but this requires crafting a variational inference procedure tailored to this problem, and I haven't seen this published yet). The idea of a Spike-and-Slab prior, originally proposed in the 80s and refined in the 90s, is older than Lasso. It is seeing renewed interest from practitioners - for e.g. this work out of Google, sets up a variable selection problem in terms of a spike-and-slab prior with MCMC for inference. 
