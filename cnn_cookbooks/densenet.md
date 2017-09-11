---
layout: page
title: DenseNet
permalink: /densenet/
---

* [code](https://github.com/liuzhuang13/DenseNet) (including *Torch*, *PyTorch*, *Tensorflow*, *MXNet* and *Caffe*)

------

**My little words**

Before DenseNet, there exit two popular types of network architectures. One is inception-x, the other is residual-x. People are curious about how to combine them. I think DenseNet is the one that well combine the intuitions of inception-x and residual-x.

------

**The advantages of DenseNet**  

* alleviate the vanishing-gradient problem, easy to train 
* strengthen feature propagation  
* encourage feature reuse  
* reduce the number of parameters, as there is no need to re-learn redundant feature-maps
* have a regularizing effect, which reduces overfitting on tasks with smaller training set sizes

**Main idea**  

<div align="center">
<img src="http://othl3wan7.bkt.clouddn.com/densenet.png" height="136" width="692">
</div>


#### Reference:
* [Densely Connected Convolutional Networks](https://arxiv.org/abs/1608.06993)