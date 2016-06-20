---
layout: page
title: Softmax
permalink: /softmax/
---

------

The **softmax function** is given by

$$\sigma (\mathbf{z})_{i}={\frac {e^{z_{i}}}{\sum_{k=1}^{K}e^{z_{k}}}}$$
for $$i=1,\dots,K.$$  

The derivative $$\frac{\partial \sigma(\mathbf{z})_{i}}{\partial \mathbf{z}_{j}}$$ of the softmax function  
if $$i=j:$$  
$$
\frac{\partial \sigma(\mathbf{z})_{i}}{\partial \mathbf{z}_{j}}
=
\left(\frac {e^{z_{j}}}{\sum _{k=1}^{K}e^{z_{k}}}\right)^{\prime}
=
\frac { \left(\sum_{k=1}^{K}e^{z_{k}}\right) \left(e^{z_{j}}\right)^{\prime} - \left( \sum_{k=1}^{K}e^{z_{k}} \right)^{\prime} e^{z_{j}} } { \left(\sum_{k=1}^{K}e^{z_{k}}\right)^2 } 
=
\frac { \left(\sum_{k=1}^{K}e^{z_{k}}\right) \left(e^{z_{j}}\right) - e^{z_{j}}e^{z_{j}} } { \left(\sum_{k=1}^{K}e^{z_{k}}\right)^2 } 
$$


#### Reference:
* [Wiki](https://en.wikipedia.org/wiki/Softmax_function)
* [Softmax vs. Softmax-Loss: Numerical Stability](http://freemind.pluskid.org/machine-learning/softmax-vs-softmax-loss-numerical-stability/)