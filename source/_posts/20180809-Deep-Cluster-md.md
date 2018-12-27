---
title: Deep Clustering for Unsupervised Learning of Visual Features - Notes
date: Thu 09 Aug 2018 05:27:34 PM PDT
categories: Research
tags:
- feature learning
- unsupervised learning
---

Unrelated:
在国内待了20多天,家里又热又潮,非常怀疑自己在七月回国的决定..

Related:

This paper iteratively updates the convnet's weights and clustering results, which help each other to get better classification performances on ImageNet. Very similar to my master thesis, even the choice of AlexNet and Kmeans. But this paper's approach is robust and scalable on different datasets.

<figure>
    <img src="https://cl.ly/3r0P3I2x3z1V/Image%202018-08-10%20at%208.31.57%20AM.png">
    <figcaption style="text-align: center;">Pipeline from this paper</figcaption>
</figure>

#### Key processings:

1. Remove colors by a fixed linear transformation based on Sobel filters **[link][1]** **[link][2]**. This might be the main reason why my experiments failed, because convnets can easily learn the information most related to colors if we use RGB images. And colors are not that important in image classification tasks.
2. Remove LRN layers in AlexNet and replace them with batch-norm layers
3. Apply a center cropping to images and perform data augmentations including random horizontal flips, crops of random sizes and aspect ratios
4. For clustering, every feature vector is dim-reduced to 256 dims by PCA
5. Reassign the clusters after every epoch for 500 epochs
6. According to [reddit][4], they solve the cluster id reassignment problem by reseting the last fc layer and retrain it

#### Interesting findings

1. While NMI ends at 0.8, meaning that many iamges are regularly reassigned between epochs, there's no impact on the training and the models do not diverge
2. Even the ground truth class number is 1000 for ImageNet, the model performs best when K=10000, revealing some sub-segmentation helps the performance further
3. Some filters in high layers (e.g. the last conv layer) can simply repeat the texture already learned in the previous layers. This situation agrees with that features from *conv3* or *conv4* are more discriminative than those from *conv5* **[link][3]**
4. Lower filters contain information about structures that highly relate to object classes while higher filters care more about style (more abstract)
5. As every layer's performance, *conv1* of the model trained with Deep Cluster method performs poorly, probably because features of *conv1* are mostly related to colors and the color is removed here
6. This paper suspects *conv5* layer contains the most of the class level information because that's where the difference between DeepCluster and a supervised AlexNet gains the largest value
7. When the target task is highly different from the domain covered by your training dataset (ImageNet here), labels are less important. (Straightforward)
8. Pre-training is essential in image retrieval tasks because random convnets perform particularly badly compared to pre-training models



[1]: https://arxiv.org/pdf/1505.05192.pdf
[2]: https://arxiv.org/pdf/1603.09246.pdf
[3]: https://arxiv.org/abs/1611.09842
[4]: https://www.reddit.com/r/MachineLearning/comments/90k86x/r_deep_clustering_for_unsupervised_learning_of/