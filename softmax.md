---
layout: page
title: Softmax
permalink: /softmax/
---

------

The **softmax function** is given by

$$\sigma (\mathbf{z})_{i}={\frac {e^{z_{i}}}{\sum_{k=1}^{K}e^{z_{k}}}}$$
for $$i=1,\dots,K.$$  

The derivative $$\frac{\partial \sigma(\mathbf{z})_{i}}{\partial \mathbf{z}_{j}}$$ of the softmax function  

if $$i=j:$$  
$$
\frac{\partial \sigma(\mathbf{z})_{i}}{\partial \mathbf{z}_{j}}
=
\left(\frac {e^{z_{j}}}{\sum _{k=1}^{K}e^{z_{k}}}\right)^{\prime}
=
\frac { \left(\sum_{k=1}^{K}e^{z_{k}}\right) \left(e^{z_{j}}\right)^{\prime} - \left( \sum_{k=1}^{K}e^{z_{k}} \right)^{\prime} e^{z_{j}} } { \left(\sum_{k=1}^{K}e^{z_{k}}\right)^2 } 
=
\frac { \left(\sum_{k=1}^{K}e^{z_{k}}\right) \left(e^{z_{j}}\right) - e^{z_{j}}e^{z_{j}} } { \left(\sum_{k=1}^{K}e^{z_{k}}\right)^2 } 
$$  

if $$i \neq j:$$  
$$
\frac{\partial \sigma(\mathbf{z})_{i}}{\partial \mathbf{z}_{j}}
=
\left(\frac {e^{z_{i}}}{\sum _{k=1}^{K}e^{z_{k}}}\right)^{\prime}
=
\frac { \left(\sum_{k=1}^{K}e^{z_{k}}\right) \left(e^{z_{i}}\right)^{\prime} - \left( \sum_{k=1}^{K}e^{z_{k}} \right)^{\prime} e^{z_{i}} } { \left(\sum_{k=1}^{K}e^{z_{k}}\right)^2 } 
=
\frac { 0 - e^{z_{j}}e^{z_{i}} } { \left(\sum_{k=1}^{K}e^{z_{k}}\right)^2 } 
$$


------

### Implementation in Caffe (Details)

**Forward**  
In this code, $$dim=channels*inner_num_$$. (*I am not clear why subtract the max? Avoiding large values?*) If *bottom_data* is a $$N*C*H*W$$ matrix and $$softmax_axis_=2$$, *top_data* is a $$N*C*H*W$$ matrix, *scale_data* is a $$N*C*1*W$$ matrix, *sum_multiplier_* is a $$H*1$$ identity vector.  
* caffe_cpu_gemm<Dtype>(CblasNoTrans, CblasNoTrans, channels, inner_num_, 1, -1., sum_multiplier_.cpu_data(), scale_data, 1., top_data);  
$$
top_data = (-1.)*sum_multiplier_*scale_data  + 1.*top_data
$$
* caffe_cpu_gemv<Dtype>(CblasTrans, channels, inner_num_, 1., top_data, sum_multiplier_.cpu_data(), 0., scale_data);
$$
scale_data = (1.)*top_data^{T}*sum_multiplier_ + 0.*scale_data
$$

```c++

  int channels = bottom[0]->shape(softmax_axis_);
  int dim = bottom[0]->count() / outer_num_;
  caffe_copy(bottom[0]->count(), bottom_data, top_data);
  // We need to subtract the max to avoid numerical issues, compute the exp,
  // and then normalize.
  for (int i = 0; i < outer_num_; ++i) {
    // initialize scale_data to the first plane
    caffe_copy(inner_num_, bottom_data + i * dim, scale_data);
    for (int j = 0; j < channels; j++) {
      for (int k = 0; k < inner_num_; k++) {
        scale_data[k] = std::max(scale_data[k],
            bottom_data[i * dim + j * inner_num_ + k]);
      }
    }
    // subtraction
    caffe_cpu_gemm<Dtype>(CblasNoTrans, CblasNoTrans, channels, inner_num_,
        1, -1., sum_multiplier_.cpu_data(), scale_data, 1., top_data);
    // exponentiation
    caffe_exp<Dtype>(dim, top_data, top_data);
    // sum after exp
    caffe_cpu_gemv<Dtype>(CblasTrans, channels, inner_num_, 1.,
        top_data, sum_multiplier_.cpu_data(), 0., scale_data);
    // division
    for (int j = 0; j < channels; j++) {
      caffe_div(inner_num_, top_data, scale_data, top_data);
      top_data += inner_num_;
    }
  }

```


#### Reference:
* [Wiki](https://en.wikipedia.org/wiki/Softmax_function)
* [Softmax vs. Softmax-Loss: Numerical Stability](http://freemind.pluskid.org/machine-learning/softmax-vs-softmax-loss-numerical-stability/)
* [How to implement a neural network Intermezzo 2](http://peterroelants.github.io/posts/neural_network_implementation_intermezzo02/)
* [cblas_sgemm](https://developer.apple.com/library/mac/documentation/Accelerate/Reference/BLAS_Ref/#//apple_ref/c/func/cblas_sgemm)
* [cblas_sgemv](https://developer.apple.com/library/mac/documentation/Accelerate/Reference/BLAS_Ref/#//apple_ref/c/func/cblas_sgemv)