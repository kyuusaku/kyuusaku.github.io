---
layout: page
title: ResNeXt
permalink: /resnext/
---

* [code](https://github.com/facebookresearch/ResNeXt) (including *Torch*, *PyTorch*, *MXNet* and *Caffe*)

------
**Main idea:**

<div align="center">
<img src="http://othl3wan7.bkt.clouddn.com/resnext_mainidea.png" height="331" width="559" >
</div>

A method to *increase the capacity* (#kernels) of CNNs and empirically outperforms the original ResNet module. This method provides an evidence that **grouped convolutions can improve accuracy** as well as may **reduce redundancy**. Authors also argue that it is imprecise to view this method as ensembling, because the members to be aggregated are trained jointly, not independently.

**The complexity**

* #Params. 
	* Original ResNet: $$ n_in \times n_mid + 9 $$


<div align="center">
<img src="http://othl3wan7.bkt.clouddn.com/resnext_network.png" height="696" width="546" >
</div>

#### Reference:
* [Aggregated Residual Transformations for Deep Neural Networks](https://arxiv.org/abs/1611.05431)