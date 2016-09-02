---
layout: page
title: Cross Entropy (Log Loss)
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
where  
$$
 \delta_{ij} = 
   \begin{cases}
     1 & \quad \text{if } i = j \\
     0 & \quad \text{if } i \neq j \\
   \end{cases}
$$  

*It is apparent that the label $$y_i$$ controls the importance of the loss.*


### Softmax With Loss

*Softmax with loss* is a special case of the forementioned *general cross entropy loss* with $$y_i=1$$ for $$i$$th class. 


### Sigmoid Cross Entropy Loss

In this case, $$o_i=\frac{1}{1+e^{-z_i}}$$, and sigmoid cross entropy loss will compute the losses for both the positive samples ($$y_i=1$$) and negative samples ($$y_i=0$$).
The loss, 
$$
 \ell_{i} = 
   \begin{cases}
     - \log \left( \frac{1}{1+e^{-z_i}} \right) = - \left( \log 1 - \log \left( 1+e^{-z_i} \right) \right) = - \left( - \log \left( 1+e^{-z_i} \right) \right) & \quad \text{if } y_i = 1 \\
     - \log \left( 1 - \frac{1}{1+e^{-z_i}} \right) = \log \left( \frac{e^{-z_i}}{1+e^{-z_i}} \right) = \log \left( \frac{1}{1+e^{z_i}} \right) = - \left( - \log \left( 1+e^{z_i} \right) \right) & \quad \text{if } y_i = 0 \\
   \end{cases}
$$  

Using the following equations,  
$$ - \log \left( 1+e^{-z_i} \right) = z_i - \log \left( 1+e^{z_i} \right) $$  
$$ - \log \left( 1+e^{z_i} \right) = - z_i - \log \left( 1+e^{-z_i} \right) $$  

The loss function can be fomulated as,  
$$ \ell_i = - \left( z_i (y_i - (z_i \geq 0)) - \log \left( 1 + e^{z_i - 2z_i(z_i \geq 0)} \right) \right) $$

**sample code in Caffe (Forward)**

```c++

    // Stable version of loss computation from input data
    const Dtype* input_data = bottom[0]->cpu_data();
    const Dtype* target = bottom[1]->cpu_data();
    Dtype loss = 0;
    for (int i = 0; i < count; ++i) {
      loss -= input_data[i] * (target[i] - (input_data[i] >= 0)) -
          log(1 + exp(input_data[i] - 2 * input_data[i] * (input_data[i] >= 0)));
    }
    top[0]->mutable_cpu_data()[0] = loss / num;

```

The derivative is   
$$
\frac {\partial \ell} {\partial z_{i}}
=
\frac {\partial \ell} {\partial o_i} \frac {\partial o_i} {\partial z_{i}}
=
- \frac {y_i} {o_i} \left( o_i \left( 1 - o_i \right) \right)
=
- \left( y_i - o_i \right)
$$

**sample code in Caffe (Backward)**

```c++

    const int count = bottom[0]->count();
    const int num = bottom[0]->num();
    const Dtype* sigmoid_output_data = sigmoid_output_->cpu_data();
    const Dtype* target = bottom[1]->cpu_data();
    Dtype* bottom_diff = bottom[0]->mutable_cpu_diff();
    caffe_sub(count, sigmoid_output_data, target, bottom_diff);
    // Scale down gradient
    const Dtype loss_weight = top[0]->cpu_diff()[0];
    caffe_scal(count, loss_weight / num, bottom_diff);

```


#### Reference:
* [Wiki: Cross_entropy](https://en.wikipedia.org/wiki/Cross_entropy)
* [Softmax vs. Softmax-Loss: Numerical Stability](http://freemind.pluskid.org/machine-learning/softmax-vs-softmax-loss-numerical-stability/)

![log_x](/fig/log_x.png)