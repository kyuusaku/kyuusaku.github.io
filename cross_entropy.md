---
layout: page
title: Cross Entropy
permalink: /cross_entropy/
---

------

Given the *"true"* distribution $$p$$, the **cross entropy** between two probability distributions $$p$$ and $$q$$ over the same underlying set of events are able to measure how the *"observed"* probability distribution $$q$$ match the *"true"* distribution $$p$$.  

The cross entropy for the distributions $$p$$ and $$q$$ over a given set is defined as follows:  
$$H(p,q)=E_{p}[-\log q]=H(p)+D_{\mathrm{KL}}(p \parallel q)$$  
where $$H(p)$$ is the entropy of $$p$$, and $$D_{\mathrm{KL}}(p \parallel q)$$ is the Kullback–Leibler divergence of $$q$$ from $$p$$ (also known as the relative entropy of $$p$$ with respect to $$q$$ — note the reversal of emphasis).
For discrete $$p$$ and $$q$$ this means
$$H(p,q)=-\sum_{x}p(x) \log q(x)$$  
The situation for continuous distributions is analogous:
$$-\int_{X}p(x)\log q(x) \mathrm{d}x$$



#### Reference:
* [Wiki](https://en.wikipedia.org/wiki/Cross_entropy)