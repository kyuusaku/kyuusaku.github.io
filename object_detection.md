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
A simple yet effective online hard example mining algorithm for training any Fast R-CNN style object detector. Steps:  
```
(a) compute loss for all the input RoIs;  
(b) sort the input RoIs by loss and take the B/N examples for which the current network performs worst, where N is the number of images, B is the number of batchsize.
```

###

