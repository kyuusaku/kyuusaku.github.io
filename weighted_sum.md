---
layout: page
title: Weighted Sum
permalink: /weighted_sum/
---

------

##Global weighted sum

Given two vectors $$\mathbf{a} \in R^D$$ & $$\mathbf{b} \in R^D$$, the global weighted sum is given by  
$$
z=\sum_{d=1}^{D} a_d * b_d=a_1*b_1+\cdots+a_D*b_D.
$$  
$$
\frac{\partial z}{\partial a_d} = b_d;\frac{\partial z}{\partial b_d} = a_d.
$$