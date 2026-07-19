---
layout: page
title: ZooCAM Challenge
description: First-place solution for a large-scale plankton image classification challenge.
img:
importance: 1
category: deep-learning
github: https://github.com/giorgio-bono/ZooCAM_Challenge
---

This project was our solution to the _3-MD-4040 2026 ZooCAM Challenge_, a private Kaggle competition organized within the Deep Learning course at CentraleSupélec.

Our team, **Accord Italie France**, achieved **1st place** on the final leaderboard.

## Overview

The goal of the challenge was to classify plankton organisms from images captured by a ZooCAM imaging system. This is a difficult visual recognition problem because plankton classes can have highly variable morphology, while imaging conditions and object scales vary significantly.

The dataset contained:

- 1,215,213 total images;
- about 1,093,000 training images;
- 86 classes;
- no public labels for the test set.

The competition used **Macro F1-score** as the evaluation metric, making performance on rare classes as important as performance on frequent classes.

## Main Challenges

The dataset was extremely imbalanced. The largest class contained around 300,000 images, while the smallest had only 73 samples. To reduce the dominance of frequent classes during training, we used a `WeightedRandomSampler` with a sampling weight controlled by an exponent alpha in the range 0.25 to 0.5.

Image sizes were also highly heterogeneous, ranging from very small samples to images up to 1288 x 1288 pixels. To make CNN training feasible, images were rescaled to a fixed resolution during preprocessing.

## Method

The final solution relied on training multiple convolutional neural networks from scratch on the ZooCAM dataset and combining their predictions through an ensemble.

The main architectures were:

- ResNet50;
- EfficientNet-B3;
- ConvNeXt-Tiny.

The training pipeline used:

- `CrossEntropyLoss`;
- label smoothing between 0.05 and 0.1;
- weighted sampling to handle class imbalance;
- strong data augmentation;
- validation-based model selection.

## Test-Time Augmentation

At inference time, each model used **Test-Time Augmentation (TTA)**. Multiple augmented versions of the same image were evaluated and averaged, making predictions more robust to small visual variations.

## Ensemble Strategy

The final submission was produced with a weighted logits ensemble. For each sample, we computed a weighted sum of the logits produced by ResNet50, EfficientNet-B3, and ConvNeXt-Tiny, then applied softmax to obtain the final class prediction.

This ensemble improved the result compared to individual models and helped stabilize predictions across rare and frequent classes.

## Results

The competition included:

- 39 participants;
- 14 teams;
- 639 total submissions.

Our team achieved:

| Leaderboard         | Score       |
| ------------------- | ----------- |
| Public leaderboard  | **0.80506** |
| Private leaderboard | **0.79164** |

**Final rank: 1st place.**

We reached this result with only 15 submissions, relying on offline validation and careful experimentation rather than leaderboard probing.

## Repository Structure

The repository contains exploratory analysis, training code, inference utilities, configuration files, and submission outputs:

- `analysis/`: dataset statistics, image size analysis, class distribution analysis;
- `src/torchtmpl/`: training and inference framework;
- `models/`: implementations of the architectures tested during the competition;
- `data.py`: dataloaders, preprocessing, and augmentation transforms;
- `optim.py`: losses, optimizers, and schedulers;
- `utils.py`: training loops, validation, checkpointing, logging, and TTA;
- `model_committee.py`: weighted logits ensemble implementation;
- `outputs/`: generated CSV predictions for Kaggle submissions;
- `config-*.yaml`: training and inference configurations.

Training and validation metrics were tracked with Weights & Biases to compare models, monitor learning dynamics, and analyze validation performance.

## Links

- [GitHub repository](https://github.com/giorgio-bono/ZooCAM_Challenge)
