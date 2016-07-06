---
layout: page
title: Research map about weakly supervised learning
permalink: /weakly_supervised_learning/
---

------


> Object localization by analyzing the change in the recognition scores when feeding into different regions of the image.

* **Self-Taught** Object Localization with Deep Networks  
    They prove that:  
    for deep neural networks, when the region containing the object is artificially occluded the whole-image classification score will drop significantly. (Figure 1)  
    They use the following methods to generate bounding boxes that are very likely to contain objects:  
    + mask out image subregion by using the mean value of the individual image channels;  
    + compare the classification scores of the original image to those of the masked-out image. if the difference for the $$c$$-th class is large, the masked-out region is very discriminative for that class. Thus such region is deemed likely to contain the object of class $$c$$.


#### Attention models

> **2016**

* **Attention Correctness** in Neural Image Captioning  
    The proposed evauation metric:  
    Let $$R$$ be the groundtruth attention region, the attention correctness is $$AC=\sum_{i \in R} \alpha_{i}$$, which is a score between 0 and 1. $$\alpha_{i}$$ is resized and normalized in order to ensure size consistency. The baseline score is simply the percentage of the bounding box size over the size of the whole image. Draw histograms of attention correctness.  


