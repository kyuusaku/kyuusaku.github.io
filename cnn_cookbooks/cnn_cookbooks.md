---
layout: page
title: CNN Cookbooks
permalink: /cnn_cookbooks/
---

Convolutional neural networks (CNNs) are currently widely used in many applications, such as face recognition, autonomous vehicles, etc. CNNs are so important to be able to change our daily lives. Therefore I am collecting everything about CNNs here for quick references.  

CNNs are conducted on many basic fucntional blocks and adjusted by learning strategies. In order to apply CNNs on mobile devices, there also came out a lot of works for reducing computation costs of CNN. I am collecting all the existing techniques. I wrote notes for some of them and given the reference papers for the ones that are in progress.


## Basic blocks
------
* **Convolutions**
	* [convolution]()
	* [atrous convolution]()
	* [deconvnet](/deconvnet/)
	* [group convolution]()
	* [depthwise separable convolution]()
	* [pointwise convolution]()
	* [pointwise group convolution]()


* **Pooling**
	* [global average pooling]()
	* [weighted sum](/weighted_sum/)


* **Activations**
	* [ReLU](/relu/)


* **Losses** 
	* [softmax](/softmax/)
	* [cross entropy loss (log loss)](/cross_entropy/)
	* [triplet loss]() *Coming soon!*
	* [contrastive loss]() *Coming soon!*


## Architectures
-------

* **General models for classification**
	* [ResNet]() *by Kaiming He*	
	* [ResNeXt]()
	* [Inceptions]() *by Google*
	* [Xception](/xception/) *by Google*
	* [VGG]()	
	* [AlexNet]()

* **Low computation cost design**
	* [ShuffleNet](/shuffle_net/) *by Face++*
	* [MobileNet](/mobile_net/) *by Google*
	* [SqueezeNet]()

* **Compression techniques**
	* [Pruning network connections[6, 7] or channels]()
	* [Quantization[28, 24, 36, 40] and factorization[20, 15, 17, 34]]()
	* [FFT[23, 32] and other methods[2]]()
	* [Distilling[11] transfer]()


* **Segmentation**




## Learning strategies
-------
* [dropout](/dropout/)


http://sebastianruder.com/optimizing-gradient-descent/