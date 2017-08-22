---
layout: page
title: ResNeXt
permalink: /resnext/
---

* [code](https://github.com/facebookresearch/ResNeXt) (including *Torch*, *PyTorch*, *MXNet* and *Caffe*)

------
**Main idea**  

<div align="center">
<img src="http://othl3wan7.bkt.clouddn.com/resnext_mainidea.png" height="331" width="559" >
</div>

and the real implementation  

<div align="center">
<img src="http://othl3wan7.bkt.clouddn.com/resnext_implement.png" height="196" width="140" >
</div>


A method to *increase the capacity* (#kernels) of CNNs and empirically outperforms the original ResNet module (1~2% point, small nets are better). This method provides an evidence that **grouped convolutions can improve accuracy** as well as may **reduce redundancy**. Authors also argue that it is imprecise to view this method as ensembling, because the members to be aggregated are trained jointly, not independently.

**The complexity**

* #Params. 
	* Original ResNet: $$ d_{in} \times d_{mid} + 9d_{mid}^2 + d_{mid} \times d_{out} \approx 17d_{mid}^2$$
	* ResNeXt: $$ d_{in} \times 2d_{mid} + 32\times9(\frac{2d_{mid}}{32})^2 + 2d_{mid} \times d_{out}  \approx 16\frac{9}{8}d_{mid}^2$$  

<div align="center">
<img src="http://othl3wan7.bkt.clouddn.com/resnext_network.png" height="696" width="546" >
</div>

#### Reference:
* [Aggregated Residual Transformations for Deep Neural Networks](https://arxiv.org/abs/1611.05431)