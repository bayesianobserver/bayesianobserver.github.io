Weight decay and L2 regularization are closely related concepts and are often used interchangeably in discussions about neural network training, but they are not exactly the same, particularly when considering different optimizers such as SGD, Adam, and AdamW. The distinction mainly arises from how the regularization is implemented in the optimization algorithm.

L2 Regularization
L2 regularization directly modifies the loss function by adding a penalty term equal to the square of the magnitude of the weights. This penalty term is scaled by a regularization coefficient (often denoted as λ). The gradient of the loss function then inherently includes the effect of this regularization:

 
Gradient with respect to weights 
�
Gradient with respect to weights w: 

This approach is straightforward and applies universally, regardless of the optimizer being used.

Weight Decay
Weight decay was originally proposed as a method to decay the weights by a small factor directly during the weight update, rather than as part of the gradient of the loss function. In the context of the simplest optimizer, SGD, weight decay and L2 regularization are effectively the same because the weight update with weight decay looks like this:

η is the learning rate. This update rule mimics the effect of having added an L2 penalty to the loss function.

Distinctions with Adam and AdamW
The distinction between L2 regularization and weight decay becomes significant with optimizers that adaptively adjust learning rates per parameter, such as Adam. With Adam, L2 regularization is applied to the running averages of past squared gradients (the second moments), which can lead to different behavior than traditional weight decay:

Adam with L2 Regularization: The L2 penalty influences both the gradients and the adaptive learning rates. This can lead to less effective regularization, especially for parameters that have small gradients.
AdamW: This is a variant of Adam that decouples weight decay from the gradient updates. Here, weight decay is applied directly to the weights after the adaptive learning rate has been applied to the gradients, which restores the original intention of weight decay even in the presence of adaptive learning rates. This tends to lead to better training outcomes for models, particularly those that benefit from regularization (e.g., in tasks with fewer data points or higher complexity).
