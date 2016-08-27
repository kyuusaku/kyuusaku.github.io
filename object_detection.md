---
layout: page
title: Research map about object detection
permalink: /object_detection/
---

------

### Frameworks

> **2016**

* **R-FCN**: Object Detection via Region-based Fully Convolutional Networks
[paper](http://arxiv.org/abs/1605.06409) 
[code](https://github.com/daijifeng001/r-fcn)  
Key: position-sensitive score maps & position-sensitive RoI pooling. (refer Figure2,3,4)  
Solve problem: the dilemma of increasing translation *invariance* for image classification vs. respecting translation *variance* for object detection.

* **SSD** Single Shot MultiBox Detector   



* **Fast R-CNN with Online Hard Example Mining (OHEM)** 
[paper](http://arxiv.org/abs/1604.03540)  
A simple yet effective online hard example mining algorithm for training any Fast R-CNN style object detector. 2.6% improvement. Steps:  
	+ compute loss for all the input RoIs;  
	+ sort the input RoIs by loss and take the B/N examples for which the current network performs worst, where N is the number of images, B is the number of batchsize. (*use standard NMS to perform deduplication. Given a list of RoIs and their losses, NMS works by iteratively selecting the RoI with the highest loss, and then removing all lower loss RoIs that have high overlap with the selected region. They use a relaxed IoU threshold of 0.7 to suppress only highly overlapping RoIs*)

> **2015**

* **DenseBox**


* **YOLO** [project](http://pjreddie.com/darknet/yolo/)  
    They frame object detection as a regression problem to spatially separated bounding boxes and class probabilities. 

* Object Detection Networks on Convolutional Feature Maps
[paper](http://arxiv.org/abs/1504.06066)  
This paper demonstrates that carefully designing deep networks for object classification is just as important. About 2% improvement. (proposed method: refer Figure 1)

* **Faster R-CNN**
[matlab code](https://github.com/ShaoqingRen/faster_rcnn)
[python code](https://github.com/rbgirshick/py-faster-rcnn)


* **Fast R-CNN**
[paper]()
[python code](https://github.com/rbgirshick/fast-rcnn)


> **2014**

* **R-CNN**

------

### Proposals

> top-down pipeline  



> segmentation-based algorithms  

* **MCG** (Multiscale Combinatorial Grouping)

* **selective search**  

* **Randomized Prim**

* **Geodesic**


> measure objectness  

$$how likely an image window is an object?$$

* **What is an object?**  

* **BING**  

* **Edgeboxes**  
    bounding boxes which have fewer contours straggling the boundary of the box are considered more likely to be objects.  

* **DeepProposal**: Hunting Objects by Cascading Deep Convolutional Layers 
[paper](http://arxiv.org/abs/1510.04445) 
[code](https://github.com/aghodrati/deepproposal)  

    Use linear SVM to train a proposal detector based on CNN features. A little higher recall. Similar to BING. (many training details, see the paper) (AlexNet)  

* **DeepBox** Learning Objectness with Convolutional Networks 
[paper](http://arxiv.org/abs/1505.02146) 
[code](https://github.com/weichengkuo/DeepBox)  
    They believe that *objectness* is in fact a high level construct. They train a CNN to rerank proposals produced by *Edgeboxes*. (*Demonstrating that low-level information is not sufficient to describe objectness*) (ablation from AlexNet) The training procedure consists of two stages (see 3.3).  