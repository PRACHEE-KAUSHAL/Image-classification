# Image-classification

# ResNet-Based Image Classification
**Group Number: 9**

## Overview
This project implements a modified ResNet model for CIFAR-100 image classification.  
We focused on improving accuracy through learning rate tuning, optimizer comparison, data augmentation, and regularization.  
We also analyzed model behavior using Saliency Maps and Grad-CAM.

---

## Dataset
- CIFAR-100
- 100 classes
- Image size: 32×32
- 500 images per class

Since ResNet is designed for larger images (224×224), the first convolution layer was modified to adapt to smaller inputs.

---

## Experiments & Results

### Learning Rate Tuning
| Learning Rate | Accuracy |
|---------------|----------|
| 0.1           | 0.58     |
| 0.01          | 0.65     |
| 0.001         | **0.71** |

Lower learning rate improved convergence and performance.

### Optimizer Comparison
- SGD performed better than Adam.
- Adam without augmentation → ~0.50 accuracy.
- Adam + Dropout → further reduced performance.

### Regularization
- Dropout reduced overfitting.
- Data augmentation improved validation accuracy more effectively.

---

## Explainability Analysis
We used:
- Saliency Maps
- Grad-CAM

Observations:
- Model often focused more on background than main object.
- Misclassifications were caused by background bias.
- Average saliency score observed ≈ 0.39.

---

## Failure Analysis
Main challenges:
- Small image size (32×32)
- Limited images per class
- Overfitting in early experiments

Dropout and data augmentation reduced the train–validation gap.

---

## Final Outcome
- Best Accuracy Achieved: **0.71**
- Best Learning Rate: **0.001**
- Best Optimizer: **SGD**

---

## Key Takeaways
- Learning rate tuning significantly impacts performance.
- Data augmentation improves generalization.
- Dropout reduces overfitting but may reduce peak accuracy.
- Explainability tools help identify model weaknesses.
