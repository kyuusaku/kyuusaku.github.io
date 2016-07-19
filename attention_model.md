---
layout: page
title: Attention models
permalink: /attention_model/
---


------

Humans focus attention selectively on parts of the visual space to acquire information when and where it is needed, and combine information from different fixations over time to build up an internal representation of the scene [18], guiding future eye movements and decision making.  

* reduce the computation  
* reduce the task complexity (the object of interest can be placed in the center of the fixation and irrelevant features of the visual environment (“clutter”) outside the fixated region are naturally ignored)

> **2016**



* **Attention Correctness** in Neural Image Captioning  
    The proposed evauation metric:  
    Let $$R$$ be the groundtruth attention region, the attention correctness is $$AC=\sum_{i \in R} \alpha_{i}$$, which is a score between 0 and 1. $$\alpha_{i}$$ is resized and normalized in order to ensure size consistency. The baseline score is simply the percentage of the bounding box size over the size of the whole image. Draw histograms of attention correctness.  

* Generating Images from Captions with Attention (*Interesting work*)  
    Extension of **DRAW**,that is  **alignDRAW**, which combined **SAM**.

* Attention to Scale: Scale-aware Semantic Image Segmentation  
    Using **SAM** to select multi-scale features for semantic image segmentation.  

* Action Recognition Using Visual Attention  
    Application of **SAM** for action recognition.  

* Attentive Contexts for Object Detection  
    Using **SAM** to capture the global context.  

* Attentive Pooling Networks  
    Extension of **SAM**.  
    Key difference: a two-way attention mechanism for pair-wise matching problems.  

* Recurrent Attentional Networks for Saliency Detection  
    Application of **STN** for convolutional-deconvolution network.  


> **2015**


$$ Soft \quad alignment $$

* Show, Attend and Tell: Neural Image Caption Generation with Visual Attention (Equ.4,5,6)  
    Extension of SAM for image caption generation.

* **Soft Attention Model (Alignment model)** Neural Machine Translation by Jointly Learning to Align and Translate (Most Related. Refer Sec.3.1) 
[implementation](https://devblogs.nvidia.com/parallelforall/introduction-neural-machine-translation-gpus-part-3/)  
    A popular framework in NLP.

$$ Latent \quad parameter $$

* **STN**: Spatial Transformer Networks (*Google DeepMind* *Interesting work*)  
    *Problem*: CNNs are limited by the lack of ability to be spatially invariant to the input data in a computationally and parameter efficient manner. Due to the typically small spatial support for max-pooling, this spatial invariance is only realised over a deep hierarchy of max-pooling and convolutions, and the intermediate feature maps in a CNN are not actually invariant to large transformations of the input data. The limitation of CNNs is due to having only a limited, pre-defined pooling mechanism for dealing with variations in the spatial arrangement of data.  
    *Advantage*: (1) select regions of an image that are most relevant; (2) transform those regions to a canonical, expected pose to simplify inference in the subsequent layers.  

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

