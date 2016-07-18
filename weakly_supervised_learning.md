---
layout: page
title: Research map about weakly supervised learning
permalink: /weakly_supervised_learning/
---

------

### MIL

> MIL models


#### MIL in object detection  

> The following methods aim to directly train the object detectors by selecting true positive examples (MIL strategy).

> The MIL strategy results in a non-convex optimization problem; in practice, solvers tend to get stuck in local optima such that the quality of the solution strongly depends on the initialization.  


* On learning to localize objects with minimal supervision  
    Key: **smoothed latent SVM**. (SS & CNN features)  


* Weakly Supervised Object Detection with **Convex Clustering**  



#### MIL in segmentation

* Fully Convolutional Multi-Class Multiple Instance Learning 
[paper](http://arxiv.org/abs/1412.7144)  
    They cast each image as a bag of pixel-level-instances and define a pixelwise, multi-class adaptation of MIL for the loss.  
    $$(x_l,y_l)=\arg \max_{\forall (x,y)} \hat{p}_l(x,y), \forall l \in \mathcal{L}_I$$  
    $$LOSS=\frac{-1}{|\mathcal{L}_I|} \sum_{l \in \mathcal{L}_I} \log \hat{p}_l(x_l,y_l)$$

#### MIL in deep learning

* Weakly Supervised Deep Detection Networks  
    


* **GAP** Is object localization for free? – Weakly-supervised learning with convolutional neural networks  
    

> Object localization by analyzing the change in the recognition scores when feeding into different regions of the image.

* **Self-Taught** Object Localization with Deep Networks
[code](https://github.com/lorisbaz/self-taught_localization)  
    They prove that:  

    + **for pre-trained CNNs**, when the region containing the object is artificially occluded the whole-image classification score will drop significantly. (Figure 1)  

    They use the following methods to generate bounding boxes that are very likely to contain objects:  

    + use segmentation method to generate candidate regions; (*they mask out the rectangular bounding boxes enclosing the segments rather than the segments themselves. They found experimentally that if they mask out the segments, the shape information of the segment is preserved and used by the network to perform recognition, thus causing less substantial drops in classification.*)  
    + mask out image subregion by using the mean value of the individual image channels, which is effectively equivalent to zeroing out that section of the network input as well as the corresponding units in the hidden convolutional layers;  
    + compare the classification scores of the original image to those of the masked-out image. if the difference for the $$c$$-th class is large, the masked-out region is very discriminative for that class. Thus such region is deemed likely to contain the object of class $$c$$;
    + fuse regions (bottom-up) and generate windows that are likely to contain objects (top-down). (*similarly to Selective Search. For detail comparisions, please refer the paper.*)

------

### Attention models

Humans focus attention selectively on parts of the visual space to acquire information when and where it is needed, and combine information from different fixations over time to build up an internal representation of the scene [18], guiding future eye movements and decision making.  

* reduce the computation  
* reduce the task complexity (the object of interest can be placed in the center of the fixation and irrelevant features of the visual environment (“clutter”) outside the fixated region are naturally ignored)

> **2016**

* **Attention Correctness** in Neural Image Captioning  
    The proposed evauation metric:  
    Let $$R$$ be the groundtruth attention region, the attention correctness is $$AC=\sum_{i \in R} \alpha_{i}$$, which is a score between 0 and 1. $$\alpha_{i}$$ is resized and normalized in order to ensure size consistency. The baseline score is simply the percentage of the bounding box size over the size of the whole image. Draw histograms of attention correctness.  

> **2015**




* Show, Attend and Tell: Neural Image Caption Generation with Visual Attention (Equ.4,5,6)  
    Extension of SAM for image caption generation.

* **Soft Attention Model (Alignment model)** Neural Machine Translation by Jointly Learning to Align and Translate (Most Related. Refer Sec.3.1) 
[implementation](https://devblogs.nvidia.com/parallelforall/introduction-neural-machine-translation-gpus-part-3/)  
    A popular framework in NLP.

* **DRAW**: A Recurrent Neural Network For Image Generation (*Google DeepMind* *Interesting work*)
    *Advantage*: fully differentiable.  
    *Method*: an explicitly two-dimensional form of attention, where an array of 2D Gaussian filters is applied to the image, yielding an image ‘patch’ of smoothly varying location and zoom.

* Attention for Fine-Grained Categorization (*Google*)  
    Extension of **DRAM**.

* **DRAM** Multiple Object Recognition with Visual Attention (*Google*)  
    Application of **RAM** on multiple digit recognition.

> **2014**

* **RAM (Recurrent Attention Model)** Recurrent Models of Visual Attention (*Google DeepMind*)  
    *Problem*: the amount of computation scales linearly with the number of image pixels.  
    *Idea*: adaptively selecting a sequence of regions or locations and only processing the selected regions at high resolution. (similar to the baby work: on learning where to look)  
    *Method*: Based on RNN. Process input sequentially. Select the next location based on past information and the demands of the task. (see Fig.1 (B Glimpse Network)) They evaluate their model on several image classification tasks (Translated MNIST & Clutted Translated MNIST).  
    *Drawback*: the model is non-differentiable, trained using reinforcement learning.  

**Reference:**  

* [自然语言处理中的Attention Model：是什么及为什么](http://blog.csdn.net/malefactor/article/details/50550211)

