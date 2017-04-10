---
layout: page
title: Dropout
permalink: /dropout/
---

When a large feedforward neural network is trained on a small training set,
it typically performs poorly on held-out test data. At such time, you may try dropout. 


#### What is *Dropout* ?
Randomly drop units (along with their connections) from the neural network during training.  
Consider a neural network with $$L$$ hidden layers. Let $$ l \in {f_1, \dotsc, L} $$ index the hidden layers of the network. Let $$ z^{(l)} $$ denote the vector of inputs into layer $$l$$, $$y^{(l)}$$ denote the vector of outputs from layer $$l$$ ($$y^{(0)} = x $$ is the input). $$W^{(l)}$$ and $$b^{(l)}$$ are the weights and biases at layer $$l$$. With dropout, the feed-forward operation can be described as  
$$ r^{(l)}_j \sim Bernoulli(p); $$  
$$ \tilde{y}^{(l)} = r^{(l)} * y^{(l)}; $$  
$$ z^{(l+1)}_i = w^{(l+1)}_i \tilde{y}^l + b^{(l+1)}_i; $$  
$$ y^{(l+1)}_i = f(z^{(l+1)}_i). $$

#### Implementation in torch nn [3]
* During training, Dropout masks parts of the input using binary samples from a bernoulli distribution. Each input element has a probability of p of being dropped, i.e having its commensurate output element be zero.  
* Furthermore, the outputs are scaled by a factor of 1/(1-p) during training. This allows the input to be simply forwarded as-is during evaluation.

#### About dropout

* Dropout "***prevents complex co-adaptations*** in which a feature detector is only
helpful in the context of several other specific feature detectors. Instead, each
neuron learns to detect a feature that is ***generally helpful for producing the
correct answer*** given the combinatorially large variety of internal contexts in
which it must operate." [1]
* each hidden unit in a neural network trained with dropout must learn to work with a randomly chosen sample of other units. This should make each hidden unit more robust and ***drive it towards creating useful features on its own without relying on other hidden units to correct its mistakes***. [2]
* "Another way to view the dropout procedure is as a very efficient way of ***performing model averaging*** with neural networks. A good way to reduce the error on the test set is to average the predictions produced by a very large number of different networks."  [1]
* Applying dropout to a neural network amounts to ***sampling a thinned network*** from
it. The thinned network consists of all the units that survived dropout. A
neural net with n units, can be seen as a collection of 2^n possible thinned neural networks. These networks all share weights so that the total number of parameters is still O(n^2), or less. For each presentation of each training case, a new thinned network is sampled and trained. So training a neural network with dropout can be seen as ***training a collection of 2^n thinned networks*** with extensive weight sharing, where each thinned network gets trained very rarely, if at all. [2]
* Dropout can be interpreted as ***a way of regularizing a neural network by adding noise to its hidden units***. [2]

#### Connection with others
* there is an intriguing similarity between dropout and a recent theory of the role of
sex in evolution (17). One possible interpretation of the theory of mixability articulated in (17) is that sex breaks up sets of co-adapted genes and this means that achieving a function by using a large set of co-adapted genes is not nearly as robust as achieving the same function, perhaps less than optimally, in multiple alternative ways, each of which only uses a small number of co-adapted genes. This allows evolution to avoid dead-ends in which improvements in fitness require co- ordinated changes to a large number of co-adapted genes. It also reduces the proba-bility that small changes in the environment will cause large decreases in fitness a phenomenon which is known as “overfitting” in the field of machine learning. [1]

#### Tips
* For fully connected layers, dropout in all hidden layers works better than dropout in only one hidden layer and more extreme probabilities tend to be worse, which is why we have used **0.5** throughout this paper. [1]
* For the inputs, dropout can also help, though it is often better to retain more than 50% of the inputs. [1]
* It is also possible to adapt the individual dropout probability of each hidden or input unit by comparing the average performance on a validation set with the average performance when the unit is present. This makes the method work slightly better. [1]
* For datasets in which the required input-output mapping has a number of fairly different regimes, performance can probably be further improved by making the dropout probabilities be a learned function of the input, thus creating a statistically efficient “mixture of experts” (13) in which there are combinatorially many experts, but each parameter gets adapted on a large fraction of the training data. [1]


#### The history of dropout

* Dropout training was introduced by Hinton et al. [1] as a way to control overfitting by randomly omitting subsets of features at each iteration of a training procedure.

#### Reference：
[1] [Improving neural networks by preventing
co-adaptation of feature detectors]()  
[2] [Dropout: A Simple Way to Prevent Neural Networks from
Overtting]()  
[3] [nn.Dropout](https://github.com/torch/nn/blob/master/doc/simple.md#dropout)