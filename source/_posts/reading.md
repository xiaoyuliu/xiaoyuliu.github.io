---
layout: post
categories: Research
author: xiaoyuliu
date: Wed Mar 29 20:16:04 2017
title: "Rough reading"
tag:
- segmentation
- detection
- classification
---

### Semi and Weakly Supervised Semantic Segmentation Using Generative Adversarial Network

Not clear about the intuition....

> Adding large fake visual data forces real samples to be close in the feature space, enabling a bottom-up clustering process, which, in turn, improves multiclass pixel classification

Use a fully convolutional multi-class classifier to replace the traditional discriminator *D* in GAN. The classifier is going to assign each input image pixel a label from *K* semantic classes or mark it as a fake sample, so there are acturally *K+1* classes.

Fit semantic segmentation into conditional GAN, where generator and discriminator are provided with extra information (e.g., image class labeles) to driving the generator. 

![semi-supervised][1]
![weakly-supervised][2]
<figcaption class="caption">Semi-supervised & Weakly supervised onvolutional GAN architecture.</figcaption>

In general, the performance of weakly supervised architecture is better than semi-supervised one and both outperform fully-supervised methods.

### Feature Pyramid Networks for Object Detection

![building block][3]
<figcaption class="caption">Building block.</figcaption>

The bottom-up pathway is the same as the feed-forward computation of the backbone ConvNet. And the original point is the **top-down pathway and lateral connections**:

- Each lateral connection merges feature maps of the same spatial size from the bottom-up pathway and the top-down pathway. 
- For feature maps of different spatial sizes, the paper upsamples the spatial resolution by a factor of 2 on a coarser-resolution feature map and then merges it with the corresponding bottom-up map.

### Who Said What: Modeling Individual Labelers Improves Classification

> Make use of potentially valuable information about which expert produced which label and take advantage of the unique strengths of individual experts at classifying certain types of data.

Like 因材施教，：）





[1]: https://cl.ly/1G361K0I1V2j/Image%202017-03-29%20at%208.24.01%20PM.png
[2]: https://cl.ly/3i2V371S2k37/Image%202017-03-29%20at%208.24.45%20PM.png
[3]: https://cl.ly/1m253Q3q0W0s/Image%202017-03-29%20at%208.35.28%20PM.png