
# building-segmentation-and-damage-assessment
Satellite imagery-based building segmentation and damage classification using xView2 dataset.

# 🛰️ Building Segmentation and Damage Assessment from Satellite Imagery

This project is a *prototype implementation* for the *xView2 Challenge, focusing on **building segmentation* and *damage classification* from satellite imagery.  
Due to resource constraints, a *small sample subset of the xView2 dataset* was used for this proof of concept.

---

## 🧩 Problem Statement

The goal of this project is to automatically:
1. *Detect buildings* from pre-disaster satellite images.  
2. *Assess building damage* from post-disaster images.

This enables rapid disaster response and situational awareness using remote sensing data.

---

## 🚀 Project Overview

The pipeline consists of two main stages:

### 🏠 Stage 1 — Building Segmentation
- *Objective:* Detect where buildings exist in satellite images.  
- *Model:* ResNet34 (pretrained on ImageNet) used as encoder backbone.  
- *Approach:*
  - Images were *patchified* into smaller tiles for training.
  - Loss Function: *Focal + Dice Loss* (to handle class imbalance).
  - Evaluation Metric: *F1-score*.
- *Output:* Binary building mask (building vs. non-building).

---

### 🧱 Stage 2 — Damage Classification
- *Objective:* Classify cropped building patches into different *damage levels*.
- *Model:* EfficientNetB0 (pretrained on ImageNet).  
- *Input:* Cropped pre-disaster and post-disaster building pairs.
- *Approach:*
  - Used *Focal + Categorical Cross-Entropy Loss*.
  - *Harmonic F1-score* used for evaluation.
  - Applied extensive *data augmentation* to improve generalization.
- *Output:* Damage category per building (e.g., No Damage, Minor, Major, Destroyed).

---

## 🌀 Data Augmentation Strategy

To improve model generalization and address class imbalance, a *custom augmentation pipeline* was implemented:

- *Adaptive Oversampling:*  
  Underrepresented classes are oversampled dynamically based on their frequency.

- *Epoch-based Scaling:*  
  Augmentation intensity reduces gradually as training progresses to stabilize learning.

- *Class-specific Augmentations:*
  - *Classes 1–2 (Minor damage):* Light augmentations (slight rotation, brightness shift).  
  - *Class 3 (Severe damage):* Strong augmentations (rotation, zoom, shear, brightness change).  
  - *Class 0 (Background):* Moderate augmentations.  

- *Optional Mild Effects:*
  - Random Gaussian blur
  - Slight contrast variations (±10%)
  - Channel-wise sensor noise


---

## 🧠 Tech Stack

- *Language:* Python  
- *Libraries:* TensorFlow / Keras, OpenCV, Imantics, NumPy  
- *Models:* ResNet34, EfficientNetB0 (both pretrained on ImageNet)


### 🖼️ Sample Predictions

Add your output images here for visualization, for example:

| Pre-Disaster | Post-Disaster | Segmentation Mask | Damage Level |
|---------------|---------------|-------------------|---------------|


---

## 🔮 Future Work

- Train on full *xView2 dataset* for better generalization.  
- Explore stronger architectures like *U-Net++, **DeepLabv3+, or **ConvNeXt*.  
- Incorporate *change detection modules* (e.g., Siamese or Transformer-based encoders).  

---

built by astha and krupanshi
