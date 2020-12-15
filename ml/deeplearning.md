---
layout: page
title: Deep Learning
---

- Early history of deep learning's resurgence
	- The 2006 Science paper
	- 2012 imagenet
- Theoretical underpinnings 
	- Why does an over-parameterized network work?
	- Lottery ticket hypothesis
	- The issue of Memorization
	- Ideas around the loss surface
	- Double descent
- SGD and its properties
- Deep learning fitting tips and tricks
	- Batch norm
	- Early stopping
	- Dropout
	- Learning rate
- Sequence models
- Graph neural networks
- Unsupervised learning / autoencoders
- Self supervised learning
- Deep reinforcement learning
- Adversarial aspects of deep learning
	- Adversarial perturbations: are 'small' changes made to the input (imperceptible to the human eye in the case of images) that alter the predicted output (e.g. the image's class label)
	- Training data can be unintentionally or deliberately 'poisoned' in various ways - for instance by flipping some of the labels, or by biasing the data towards some classes. 	
	- Out of distribution data at test time: the behavior of a deep neural network is unpredictable if the data fed to it at test time is completely different compared to data used at training time. To be fair, this is a problem with most supervised learning methods. Most methods assume that test data comes from the same distribution as training data - this is the basis Empirical Risk Minimization as a principle to justify minimizing a loss function on training data with the expectation of doing a good job on test data.
- Noise Constrastive learning
- Attention

