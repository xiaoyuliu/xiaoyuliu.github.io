---
title: Deep Complex Networks - Crude notes
date: 2018-05-06 19:21:08
categories: Research
tags:
    - ICLR
---

This paper comes up with the key components of deep complex networks including *complex convolutions*, *complex weight initialization*. The state-of-the-art results on audio-related tasks are achieved by the complex-valued models.

### Potential of complex representations

- [Easier optimization][1]
- [Better generalization][2]
- [Faster learning][3]
- [More robust to noise][4]
- [Richer representation capacity][5]

### Contribution

- Formulate the complex batch normalization
- Complex weight initialization
- Comparison 
- State-of-the-art results on MusicNet multi-instrument music transcription dataset
- State-of-the-art results in the Speech Spectrum Prediction task on the [TIMIT][6] dataset

### Motivation

#### Improve information retrieval from associative memory

Residual networks and Hightway Networks have similar architectures to associative memories: The associate memory is provided by the identity connection for computing residuals.

Complex numbers are demonstrated to be numerically efficient and stable for information retrieval from an associative momory.[7]

#### Address gradient vanishing and exploding problems

Unitary matrices can provide a richer representation, and unitary matrices are extentions of the orthogonal matrices over the complex number field.

#### Biological importance

    The complex-valued formulation allows one to express the neuron’s output 
    in terms of its firing rate and the relative timing of its activity. The 
    amplitude of the complex neuron represents the former and its phase the 
    latter.

Possible main advantage: The ability to consider **phase** information.

#### Signal processing perspective

- For speech signals, the phase information affects the intelligibility.
- For image signals, the phase information is sufficient to recover the majority of the information from magnitudes. Because it encodes shapes, edges and orientations.

### Previous works

Previous works either only yield real-valued kernels, or are simply applied on toy tasks with some exceptions. 

### Complex Building Blocks

#### Representation

For a 2D convolutional layer that has N feature maps and N is divisible by 2. It can be represented as complex numbers by treating the first N/2 feature maps as the real components and another N/2 as the imaginary components.

#### TBC

这篇paper好难啊……
以及最近有点懒散……
反思反思……





