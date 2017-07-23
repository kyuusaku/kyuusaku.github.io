---
layout: page
title: ShuffleNet
permalink: /shuffle_net/
---

------

Modern convolutional neural networks [27, 30, 31, 29, 9, 10] usually consist of repeated building blocks with the same structure. Among them, state-of-the-art networks such as Xception [3] and ResNeXt [37] introduce efficient depthwise separable convolutions or group convolutions into the building blocks to strike an excellent trade-off between representation capability and computational cost. However, we notice that both designs do not fully take the 1 × 1 convolutions (also called pointwise convolutions in [12]) into account, which require considerable complexity. For example, in ResNeXt [37] only 3 × 3 layers are equipped with group convolutions. As a result, for each residual unit in ResNeXt the pointwise convolutions occupy 93.4% multiplication-adds (cardinality = 32 as suggested in [37]). In tiny networks, expensive pointwise convolutions result in limited number of channels to meet the complexity constraint, which might significantly damage the accuracy.


* pointwise group convolution
* channel shuffle


Compared with popular structures like [27, 9, 37], for a given computation complexity budget, our ShuffleNet allows more feature map channels, which helps to encode more information and is especially critical to the performance of very small networks.

generalizes group convolution and depthwise separable convolution in a novel form.


#### Reference:
* [ShuffleNet: An Extremely Efficient Convolutional Neural Network for Mobile Devices](https://arxiv.org/abs/1707.01083)