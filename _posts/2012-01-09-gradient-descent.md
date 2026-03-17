---
layout: post
title: "Gradient descent"
date: 2012-01-09
original_url: "https://thebayesianobserver.wordpress.com/2012/01/09/gradient-descent/"
categories: ["uncategorized"]
---
Gradient descent is used in a bewildering range of supervised machine learning areas as an optimization method to ‘fit’ a model to training data. Its use is obvious when the objective function being optimized (which is often some type of average error over the training set) is convex in the variables of optimization (which are usually the free parameters of the model one is trying to fit). However, gradient descent is (somewhat surprisingly) also used when the objective function surface is not convex! For example, in training a neural network using the back-propagation algorithm, the free parameters of the network are updated using a stochastic gradient descent over the error function surface, which is non-convex because of the non-linearities introduced by non-linear sigmoid/other neurons. Surprisingly, gradient descent seems to work fine. The reason for this is that when employing stochastic gradient descent, the weight updates are affected by noise in individual data points (this noise tends to get averaged out in batch (conventional) gradient descent), which provides the opportunity to escape from local optima wells in the objective-function surface. Due to the nonlinear sigmoid functions, the error surface typically contains many local minima wells, as in the figure below, and these minima as very close to each other. Therefore, even if one is ultimately stuck in a local minimum, it is often not too poor compared to the global minimum.

[![](/images/gradient-descent-img-1.png "wave_surface")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/01/wave_surface.png)[![](/images/gradient-descent-img-2.jpg "wave_surface_photo")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/01/wave_surface_photo.jpg)

There are a bunch of necessary steps one must take to pre-process one’s data when employing gradient descent in order to prevent crazy convergence times.

1. Normalize each input feature to have a mean of zero.
2. Normalize the dataset so that there are no linear correlations between features. This is done by projecting each point on to an orthonormal basis — this is effectively, a rotation, which can be accomplished by multiplying the input data by a matrix  containing the eigenvectors of its covariance matrix.
3. Normalize each input feature so that it has the same variance. Doing this allows one to use the same learning rate for each free parameter in the model. If the variance of each feature is different and one chose the same learning rate for each free parameter, then the convergence in some directions would be very slow, while converge in other directions would be quick.
