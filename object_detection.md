---
layout: page
title: Research map about object detection
permalink: /object_detection/
---

------

### Frameworks

> **2016**

* **Fast R-CNN with Online Hard Example Mining (OHEM)** 
[paper](http://arxiv.org/abs/1604.03540)  
A simple yet effective online hard example mining algorithm for training any Fast R-CNN style object detector. 2.6% improvement. Steps:  
+ compute loss for all the input RoIs;  
+ sort the input RoIs by loss and take the B/N examples for which the current network performs worst, where N is the number of images, B is the number of batchsize. (*use standard NMS to perform deduplication. Given a list of RoIs and their losses, NMS works by iteratively selecting the RoI with the highest loss, and then removing all lower loss RoIs that have high overlap with the selected region. They use a relaxed IoU threshold of 0:7 to suppress only highly overlapping RoIs*)


* **Faster R-CNN**
[matlab code](https://github.com/ShaoqingRen/faster_rcnn)
[python code](https://github.com/rbgirshick/py-faster-rcnn)


* **Fast R-CNN**
[paper]()
[python code](https://github.com/rbgirshick/fast-rcnn)

###

