---
layout: post
categories: Research
author: xiaoyuliu
date: Mon Jun 19 12:51:25 2017
title: "Image-to-Image Translation with Conditional Adversarial Networks - Note"
tag:
- GAN
---

This paper introduces a novel approach to learn image-to-image translation with conditional adversarial networks, which is a uniform method instead of specially designed for one dataset.

### Motivation

People are tired of defining a subtle loss function for each CNN, which is hard some time as well. Therefore, it is desirable to look for an approach in which CNN can learn features according to some high-level requirement, like "make the output indistinguishable from reality". And satisfying the high-level requirement is exactly the task of discriminator in Generative Adversarial Model(GAN). 

However, original GAN tends to learn the unknown input distribution instead of a mapping from input to output, so the paper utilizes conditional GAN(cGAN), where the condition is the relationship between any input image and the corresponding output image.

### Network

0. **Generator**

    ![generator](https://cl.ly/1Q3c2G22172q/Image%202017-06-19%20at%201.09.23%20PM.png)

    For generator, the paper uses a "U-Net"-based architecture, which is similar with encoder-decoder network. There are some skips in U-Net between each layer $i$ and $n-i$, which are helpful to share lots of low-level information between the input and output.

1. **Discriminator**

    ![discriminator](https://cl.ly/091m253Q0B32/Image%202017-06-19%20at%201.16.55%20PM.png)

    For discriminator, there are two inputs: original frame and a label map, which could be ground truth or output of generator. The comprehensive obejctive is:

    $$
    G^* = arg \underset{G}{\min}\underset{D}{\max}\mathcal{L}_{cGAN}(G, D) + \lambda\mathcal{L}_{L_1}(G)
    $$

    Where 

    $$
    \mathcal{L}_{cGAN}(G,D) = \mathbb{E}_{x,y~p_{data}(x,y)}[logD(x,y)] + \mathbb{E}_{x~p_{data}(x), z~p_z(z)}[log(1-D(x,G(x,z)))]
    $$

    $$
    \mathcal{L}_{L1}(G) = \mathbb{E}_{x,y~p_{data}(x,y), z~p_z(z)}[||y - G(x,z)||_1]
    $$

    L1 distance is used because it encourages less blurring than L2 distance and it can also help accurately capture the low frequencies.

### Summary

cGAN appears to be effective in image processing and graphic tasks, and even though it achieves some success in vision problems like semantic segmentation, simply using reconstruction losses like L1 is mostly sufficient. 

(Really impressed by the transformation performance)




