# Image-classification

# CIFAR-100 Image Classification with Model Comparison

## Overview

This repository contains the implementation of a ResNet-based image classification model trained on the CIFAR-100 dataset.

Three different concepts were applied and compared:

1. Data Augmentation  
2. Saliency Map  
3. Grad-CAM  

The purpose of this project is to compare model performance and analyze model behavior using visualization techniques.

A detailed theoretical explanation is provided in the project report.  
This README focuses on implementation and results.

---

## Dataset

Dataset: CIFAR-100  
Source: https://www.cs.toronto.edu/~kriz/cifar.html  

Loaded using:
`torchvision.datasets.CIFAR100`

Details:
- 100 classes  
- 32×32 RGB images  
- 50,000 training images  
- 10,000 test images  

---

## Model Architecture

Base Model: ResNet-18  

Modifications:
- First convolution layer adjusted for 32×32 images  
- MaxPool layer removed  
- Dropout used in selected experiments  

Loss Function: CrossEntropyLoss  
Optimizers Tested: SGD and Adam  

---

## Experiments Performed

### 1️⃣ Data Augmentation

Data augmentation techniques applied:
- Random horizontal flip  
- Random crop  
- Normalization  

Learning rates tested:
- 0.1  
- 0.01  
- 0.001  

Best Result:
Learning rate = 0.001  
Accuracy ≈ 0.71  

Observation:
Data augmentation improved generalization and reduced overfitting.  
This configuration gave the best overall performance.

---

### 2️⃣ Saliency Map

Saliency map was implemented using gradient of predicted class with respect to input image.

Steps:
- Enable gradient on input
- Backpropagate predicted class score
- Take absolute gradient
- Max across RGB channels

Purpose:
To visualize pixel-level importance.

Observation:
- Model attention was noisy.
- Accuracy was not improved.
- In several cases, model focused on background.
- Overall performance was not satisfactory.

Conclusion:
Saliency map was useful for visualization but did not improve model performance.

---

### 3️⃣ Grad-CAM

Grad-CAM was implemented using gradients from the final convolution layer.

Steps:
- Extract feature maps from last conv layer
- Compute gradients
- Weight feature maps by gradients
- Generate heatmap
- Overlay on original image

Purpose:
To understand region-level attention.

Observation:
- Attention maps were smoother than saliency.
- Model focused better on main objects.
- Accuracy was moderate and better than saliency setup.
- Performance was acceptable but not highest.

---

## Accuracy Comparison

| Method               | Accuracy |
|----------------------|----------|
| Saliency Map Setup   | Low / unstable |
| Grad-CAM Setup       | Moderate |
| Data Augmentation    | ~0.71 (Best) |

Best configuration:
- SGD optimizer
- Learning rate = 0.001
- Data augmentation enabled

---

## Repository Structure
