---
layout: post
categories: Research
author: xiaoyuliu
date: Fri Mar 24 10:32:21 2017
title: "Mask R-CNN - Notes"
tag:
- FAIR
- segmentation
- detection
---

This paper aims at building a strong baseline in *instance segmentation* as Fast/Faster R-CNN in *object detection* and Fully Convolutional Network(FCN) in *semantic segmentation*.

### Instance Segmentation

**Methods:** Bottom-up segments $\rightarrow$ Segment proposals (like region proposals in R-CNN) $\rightarrow$ Fully convolutional instance segmentation

But usually those approaches do segment proposals then recognition or classification, which is slower and more complex than *parallel* prediction of masks and class labels in this paper.

Fully convolutional instance segmentation(FCIS) aims at simultaneously addressing object classes, boxes and masks together, based on a set of position-sensitive channels. And it cannot handle with overlap well.

### Improvements Over Faster R-CNN

0. Predict segmentation masks on each ROI together with doing bbox classification and regression.
1. Propose a quantization-free layer, *RoIAlign*, to solve the disability of faster R-CNN to do pixel-to-pixel alignment, which is able to improve mask accuracy by **relative 10% to 50%**. ($\leftarrow$ I feel this is the key element)

### Improvements Over FCN

0. Decouple mask and class prediction(FCN performs per-pixel multi-class categorization, which combines segmentation and classification): 

    > We predict a binary mask for each class independently, without competition among classes, and rely on the network’s RoI classification branch to predict the category

    The paper uses *average binary cross-entropy loss* to indicate mask loss, and for each ground-truth class *k*, the corresponding loss is only defined on the *k*-th mask.(Dimension of mask: K *x* m *x* m) So there is no competition among classes, according to experiments this is better than *per-pixel softmax* and *multinomial cross-entropy* that require classes competition. And in FCIS, there is competition between ROI inside and ROI outside.

    The second stage of Mask R-CNN predicts the class label for each ROI, then generates a mask for each class. This is not contradictory with *parallel* design because they are done iteratively through one forward.


### RoIPool and RoIAlign

RoIPool or all kinds of pooling would introduce misalignments between the RoI and the extracted features, for extracting feature for the whole image, it is robust to this small translations while for pixel-accurate masks this will be harmful because doing *quantization* will cause small shift between generated mask and original instance.

<span class="evidence">How exactly does RoIPooling work?</span>

**RoIAlign**:

- Avoid any quantization, realizing alignment between mask and instance(e.g. use $x/16$ instead of $[x/16]$)
- Use bilinear interpolation on feature map
- Compared to RoIWarp, which also adopts bilinear resampling, proving the effectiveness of RoIAlign mainly comes from alignment instead of bilinear interpolation.

### Network Structure

Two networks: *backbone* for feature extraction over an entire image and *head* for bbox recognition and mask prediction.

Backbone:

- ResNet/ResNeXt
- ResNet-FPN(more effective)

And their corresponding head networks. 

<span style="background: yellow">To be discussed about the network design.</span>

















