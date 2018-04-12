---
layout: post
categories: Research
date: Tue Mar 28 19:55:17 2017
author: xiaoyuliu
title: "Aggregated Residual Transformations for Deep Neural Networks - Notes"
tag:
- resnet
- cvpr 2017
---

This paper introduces a new "dimension" except the width and depth of networks -- "cardinality", which is the number of transformations in a set.

### ResNet v.s. Inception v.s. ResNeXt

**ResNet**: Stacking building blocks of the same shape(topology).

**Inception**: Split-Transformation-Merge.

- Split the input into a few lower-dimensional embeddings
- Transform using a set of specialized filters
- Merge by concatenation

A successful multi-branch architecture, but each branch needs to be carefully customized, no matter filter numbers or sizes. It's hard to be adapted to new tasks/datasets.

**ResNeXt**: Split-Transformation-Aggregate.

- Apply a set of transformations(same topoloty), each on a low-dimensional embedding
- Aggregate the output by summation


### Difference between Inception and ResNeXt

> Our module differs from all existing Inception modules in that all our paths share the same topology and thus the number of paths can be easily isolated as a factor to be investigated.

<span class="evidence">Key words: same topology. What is same topology?</span>

### Performance

More effective to increase cardinality than going deeper or wider.

### Structure

The network consists of a stack of residual blocks, which have the same **topology** and are subjective to two rules:

0. If two blocks produce spatial maps of the same size, they share the same hyper-parameters(width and filter sizes).
1. When the spatial map is downsampled by a factor of 2, the width of the blocks is multiplied by a factor of 2. This makes sure the computational complexity is roughly the same for all blocks.
    - Here the **width** means output channel nummber according to the section *Relation to Grouped Convolutions* and *Model Capacity*.

2. The network can be interpreted as:

    $$
    F(x) = \sum_{i=1}^C T_i(x)
    $$
    Where C is the size of the set of transformations to be aggregated, is *cardinality*.$T_i(x)$ means *i*-th transformation applied on *x*. The residual block is:
    
    $$
    y = x + \sum_{i=1}^C T_i(x)
    $$

3. Reformulation

![reformulation][1]
<figcaption class="caption">Equivalent building blocks of ResNeXt</figcaption>

(b) seems similar to Inception-ResNet block because it involves branching and concatenationg in the residual function. But different in **sharing the same topology among the multiple paths** in ResNext.

(c) uses the natotaion of grouped convolutions, which is supposed to be introduced by AlexNet for the first time, just for distributing the task to two GPUs, and no evidence to speed up training.

(b) and (c) are equivalant reformulations to (a), but for (c) when the block has a depth smaller than 3, there's no meaning to use (c) reformulation except **leading to a trivially wide and dense model**. <span class="evidence">Is that because for a two-layer block there is no chance to divide the input channels to groups? Having no middle layer in (c).</span>


[1]: https://cl.ly/422f3m3s1v1d/Image%202017-03-28%20at%208.59.04%20PM.png







