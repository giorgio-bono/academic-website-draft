---
layout: page
title: ZooCAM Challenge
description: First-place solution for a large-scale plankton image classification challenge.
img:
importance: 1
category: deep-learning
redirect: https://github.com/giorgio-bono/ZooCAM_Challenge
---

First-place solution for the CentraleSupélec Deep Learning Kaggle challenge _3-MD-4040 2026 ZooCAM Challenge_. The task focused on plankton image classification with 1.2M samples and 86 classes.

The solution used CNNs trained from scratch and a weighted logits ensemble of ResNet50, EfficientNet-B3, and ConvNeXt-Tiny, with label smoothing, weighted sampling, and test-time augmentation.

**Tools and topics:** PyTorch, CNNs, ResNet50, EfficientNet-B3, ConvNeXt-Tiny, ensemble learning, TTA.
