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

Note that the denominator of the derivative is the output $$o$$, which may cause the overflow problem when $$o$$ approaches $$0$$. 

### Softmax With Loss



### Sigmoid Cross Entropy Loss


#### Reference:
* [Wiki](https://en.wikipedia.org/wiki/Cross_entropy)