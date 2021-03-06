---
layout: page
title: Multiple Instance Learning
permalink: /multi_instance_learning/
---

In statistical pattern recognition, it is usually assumed that a training set of labeled patterns is available where each pair $$(\mathbf{x}_i,y_i)$$. Multiple-instance learning (MIL) makes significantly weaker assumptions about the labeling information. Patterns are grouped into *bags* and a label is attached to each bag and not to every pattern.


------


### Models

> **2002**

* Support Vector Machines for Multiple-Instance Learning  
    
    **mi-SVM**  

    $$ \min_{y_i}\min_{\mathbf{w},b,\xi} \frac{1}{2} \| \mathbf{w} \| + C \sum_i \xi_i $$  

    $$ s.t. \forall i : y_i(\langle \mathbf{w}, \mathbf{x}_i \rangle + b) \geq 1 - \xi_i, \xi_i \geq 0, y_i \in \{-1,1\} $$  

    $$ and \sum_{i \in I} \frac{y_i+1}{2} \geq 1, \forall I s.t. Y_I=1, y_i = -1, \forall I s.t. Y_I = -1 $$

    Notice that in the standard classification setting, the labels $$y_i$$ of training patterns $$\mathbf{x}_i$$ would simply be given, while in MIL labels $$y_i$$ of patterns $$\mathbf{x}_i$$ not belonging to any negative bag are treated as unknown integer variables. The mi-SVM formulation leads to a mixed integer programming problem. One has to find both the optimal labeling and the optimal hyperplane.  

    * Pseudo-code for mi-SVM optimization heuristics *   
    initialize $$y_i=Y_I$$ for $$i \in I$$
    

    **MI-SVM**  



------

### Applications in Joint Localization & Classification

> **2016**

* **WELDON**: Weakly Supervised Learning of Deep Convolutional Neural Networks  
    Key difference:  
    1. negative evidence scoring and top instance selection. The intuition behind top instance selection increases the risk of selecting outliers, guiding the training of the deep CNN towards bad local minima. Negative selection means using regions which best support the absence of the class.  
    2. the deep CNN is trained to optimize Average Precision.


> **2009**

* Weakly supervised discriminative localization and classification: a joint learning process  
    


### Applications in Object Detection  

> The following methods aim to directly train the object detectors by selecting true positive examples (MIL strategy).

> The MIL strategy results in a non-convex optimization problem; in practice, solvers tend to get stuck in local optima such that the quality of the solution strongly depends on the initialization.  


* On learning to localize objects with minimal supervision  
    Key: **smoothed latent SVM**. (SS & CNN features)  


> **2015**

* Weakly Supervised Object Detection with **Convex Clustering**  





### Applications in Segmentation  

* Fully Convolutional Multi-Class Multiple Instance Learning 
[paper](http://arxiv.org/abs/1412.7144)  
    They cast each image as a bag of pixel-level-instances and define a pixelwise, multi-class adaptation of MIL for the loss.  
    $$(x_l,y_l)=\arg \max_{\forall (x,y)} \hat{p}_l(x,y), \forall l \in \mathcal{L}_I$$  
    $$LOSS=\frac{-1}{|\mathcal{L}_I|} \sum_{l \in \mathcal{L}_I} \log \hat{p}_l(x_l,y_l)$$


### MIL in CNN

> **2016**

* Weakly Supervised Object Localization with Progressive Domain Adaptation  
    Their key observation is that it is hard to train object detectors directly under weak supervisory signals due to the substantial amount of noise in the object proposal collections. 
    Two main steps:  


> **2015**

* Detector Discovery in the Wild: Joint Multiple Instance and Representation Learning  
    Joint training over both weak and strong labels and which transfer learned perceptual representations from strongly-labeled auxiliary tasks. They assume that the set of object categories that appear in the weakly labeled set, do not overlap with the set of object categories that appear in the strongly labeled set. (Method: Figure2, AlexNet, ILSVRC13 Detection Dataset, Caffe)  
    Drawback: complex alternating minimization process.

* Deep Multiple Instance Learning for Image Classification and Auto-Annotation  
    *Dual multi-instance assumption*: object proposals and possible text annotations of am image can be regarded as two instance sets. (PASCAL VOC, MIT Indoor, Scene 67)

* Weakly Supervised Deep Detection Networks  



* **GMP** Is object localization for free? – Weakly-supervised learning with convolutional neural networks

* **GAP** Learning Deep Features for Discriminative Localization

    
    

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