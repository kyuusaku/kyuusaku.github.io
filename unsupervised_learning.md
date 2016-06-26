---
layout: page
title: Unsupervised learning
permalink: /unsupervised_learning/
---

* Unsupervised Learning of Edges 
[paper](http://arxiv.org/abs/1511.04166)


* Unsupervised Learning of Visual Representations using Videos
[project](http://www.cs.cmu.edu/~xiaolonw/unsupervise.html)  
They try to answer the following questions:  
	+ is strong-supervision necessary for training these CNNs?
	+ Do we really need millions of semantically-labeled images to learn a good representation?  
*It seems humans can learn visual representations using little or no semantic supervision.*
They argue that static images themselves might not have enough information to learn a good visual representation.  
*In fact, humans also learn their visual representations not from mil-lions of static images but years of dynamic sensory inputs.*  
Method:  
	+ track millions of “moving” patches in hundreds of thousands of videos; (*The key idea is that two patches connected by a track should have similar visual representation in deep feature space since they probably belong to the same object.*)
	+ train a Siamese-triplet network with ranking loss; (*This ranking loss function enforces that in the final deep feature space the first frame patch should be much closer to the tracked patch than any other randomly sampled patch.*)
	+ transfer the learned representations to the tasks with supervised data.
