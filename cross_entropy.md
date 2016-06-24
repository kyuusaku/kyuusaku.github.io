---
layout: page
title: Cross Entropy
permalink: /cross_entropy/
---

------

Given the *"true"* distribution $$p$$, the **cross entropy** between two probability distributions $$p$$ and $$q$$ over the same underlying set of events are able to measure how the *"observed"* probability distribution $$q$$ match the *"true"* distribution $$p$$.  

The cross entropy for the distributions $$p$$ and $$q$$ over a given set is defined as follows:  
$$H(p,q)=E_{p}[-\log q]=H(p)+D_{\mathrm{KL}}(p \parallel q)$$  
where $$H(p)$$ is the entropy of $$p$$, and $$D_{\mathrm{KL}}(p \parallel q)$$ is the Kullback–Leibler divergence of $$q$$ from $$p$$ (also known as the relative entropy of $$p$$ with respect to $$q$$ — note the reversal of emphasis).  

For discrete $$p$$ and $$q$$ this means 
$$H(p,q)=-\sum_{x}p(x) \log q(x)$$  

The situation for continuous distributions is analogous:
$$-\int_{X}p(x)\log q(x) \mathrm{d}x$$

------

Notes of the implementation in CNN.

### General Cross Entropy Loss

When comparing a distribution $$q$$ against a fixed reference distribution $$p$$, cross entropy and KL divergence are identical up to an additive constant (since $$p$$ is fixed): both take on their minimal values when $$p=q$$, which is $$0$$ for KL divergence, and $$H(p)$$ for cross entropy.  

Thus, for learning and optimization, we expect the output distribution $$o$$ match the label distribution $$y$$, we can minimize the following loss function:  
$$ \ell (y,o) = -\sum_{i} y_i \log \left( o_i \right) $$

The derivative $$\ell (y,o)$$ with respect to $$o_i$$ is  
$$ 
\frac {\partial \ell} {\partial o_i} 
= 
\left( -\sum_{i} y_i \log \left( o_i \right) \right)^{\prime} 
=
- \frac {y_i} {o_i}
$$  

Note that the denominator of the derivative is the output $$o_i$$, which may cause the overflow problem when $$o_i$$ approaches $$0$$. Two tricks can be used to solve this problem. One is setting a numerical lower bound.  

**sample code in Caffe**

```c++

    int num = bottom[0]->num();
    int dim = bottom[0]->count() / bottom[0]->num();
    caffe_set(bottom[0]->count(), Dtype(0), bottom_diff);
    const Dtype scale = - top[0]->cpu_diff()[0] / num;
    for (int i = 0; i < num; ++i) {
      int label = static_cast<int>(bottom_label[i]);
      Dtype prob = std::max(
          bottom_data[i * dim + label], Dtype(kLOG_THRESHOLD));
      bottom_diff[i * dim + label] = scale / prob;
    }

```

The other is re-compute the derivative with the concrete function of $$o$$. The latter is better and commonly used.  

For example, if $$ o_i = \frac {e^{z_i}} {\sum_{k=1}^{K}e^{z_{k}}} $$, (refer [softmax function](/softmax/)), the derivative of the softmax with cross entropy loss is  
$$
\frac {\partial \ell} {\partial z_{j}}
=
\frac {\partial \ell} {\partial o_i} \frac {\partial o_i} {\partial z_{j}}
=
- \frac {y_i} {o_i} \left( o_j \left( \delta_{ij} - o_i \right) \right)
=
- \frac {y_i o_j \delta_{ij}} {o_i} + y_i o_j
=
y_i \left( o_j - \delta_{ij} \right)
$$


### Softmax With Loss



### Sigmoid Cross Entropy Loss


#### Reference:
* [Wiki](https://en.wikipedia.org/wiki/Cross_entropy)