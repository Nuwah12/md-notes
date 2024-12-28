## Autoencoders

### Introduction

An autoencoder uses a hidden layer $h$ that describes a code used to represent the input. It may be viewed as consisting of 2 parts: an encoder function $h=f(x)$ and a decoder that produces a reconstruction $x'=g(h)$. Autoencoders are designed to be unable to copy input perfectly, as this would not be a useful model. Since the model is forced to prioritize which aspects of the input should be copied, it often learns useful properties of the data.  
Most autoencoders have generalized these ideas of encorders and decoders beyond deterministic functions to stochastic mappings $p_{encoder}(h|x)$ and $p_{decoder}(x|h)$.  
Autoencoders may be thought of as being a special case of feedforward networks and can be trained with all the same techniques (typically minibatch gradient descent following gradients calculated by back propogation).

### Undercomplete Autoencoders

We are not typically interested in the output of the decoder, instead, we hope that training the autoencoder to perform the input copying task will result in $h$ taking on useful properties.  
An autoencoder whose code ($h$) dimension is less than its input simension ($x$) is called **undercomplete**. Learning an undercomplete representation of the input data forves the autoencoder to capture the most salient features from the inout $x$.  
The general learning process for an autoencoder is described simply as minimizing a loss function:

$$
L(\boldsymbol{x},g(f(\boldsymbol{x})))
$$

where $L$ is a loss function penalizing the decoder for being dissimilar from $\boldsymbol{x}$, such as the mean squared error.  
**When the decoder is linear and $L$ is the mean squared error, the undercomplete autoencoder learnins to span the same subspace as PCA.** In this case, an autoencoder trained to perform the task of copying the input data has learning the principal subspace of the training data as a side effect. Thus, autoencoders with nonlinear encoder functions $f$ and nonlinear encoder functions $g$ can learning a more powerful nonlinear generalization of PCA. However, if the autoencoder is given too much capacity, it fails to learn anything useful about the data.

### Regularized Autoencoders

Undercomplete autoencoders, when given too much capacity, fail to learn anything useful from the data. In this case, capacity refers to the number of layers that comprise the encpder and decoder. For example, a very powerful, high-capacity encoder could represent data as a single-dimension code $i$, but this representation wouldn't be useful for any practical reasons. The same is true for **overcomplete** autoencoders, whose hidden code dimensions are greater than the input dimension, except here even a linear encoder and decoder can learn to copy the input to the output without learning anything useful about the input data. **Regularized Autoencoders**, rather than limiting ghe model capacity by keeping encoders and decoders shallow/code size small, use a loss function that enxourages the model to have other properties other than its ability to copy input to output. These other properties include sparsity of the representation, smallness of the derivative of that representattion, and robustness to noise or to missing inputs. 

#### Sparse Autoencoders
A sparse autoencoder is an autoenoder whose training criterion involves a sparsity penalty $\Omega(\boldsymbol{h})$ on the code layer $\boldsymbol{h}$, in addition to the previously described reconstruction error:
$$
L(\boldsymbol{x},g(f(\boldsymbol{x}))) + \Omega(\boldsymbol{h})
$$
where $g(\boldsymbol{h})$ is the decoder output, and typically $\boldsymbol{h}=f(\boldsymbol{x})$, the encoder output.
Sparse autoencoders are usually used to learn features for another task, like classification. \
We can think of $\Omega(\boldsymbol{h})$ as a regulariztion term added to a feedforward network whose 