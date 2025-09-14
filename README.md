# Attention-Enhanced CNN for Monkeypox and Related Skin Lesion Classification

This repository contains the implementation of an **Attention-Enhanced Convolutional Neural Network (CNN)** for the classification of Monkeypox and other skin lesions, based on the **Mpox Skin Lesion Dataset (MSLD v2.0)**. The experiment integrates advanced augmentation, aggressive oversampling, focal loss, and attention mechanisms to achieve robust classification across **six skin conditions**.

---

## 🔬 Overview
The project addresses the challenge of imbalanced and visually similar skin lesion datasets by combining:
- **Custom augmentations per class** (stronger augmentation for underrepresented diseases like Cowpox and Chickenpox).  
- **Aggressive oversampling** to mitigate class imbalance.  
- **Attention module (Enhanced Dot-Product Attention)** integrated into a **ResNet50 backbone**.  
- **Two-stage training strategy** with **focal loss** and **cosine annealing warm restarts**:
  1. **Stage 1** – Minority class–focused training with oversampling.  
  2. **Stage 2** – Balanced fine-tuning with standard splits.  

---

## 📂 Dataset
- **Source**: Mpox Skin Lesion Dataset v2.0 (MSLD-v2.0)  
- **Classes**:  
  1. Monkeypox  
  2. Chickenpox  
  3. Cowpox  
  4. Measles  
  5. Hand-Foot-Mouth Disease (HFMD)  
  6. Healthy  

- **Cleaning**: Duplicates removed using MD5 hashing.  
- **Final Size**:  
  - **754 images** after deduplication  
  - Split into **Train (527)**, **Validation (151)**, **Test (76)**  

---

## ⚙️ Model Architecture
- **Base Model**: ResNet50 (ImageNet pretrained)  
- **Attention Layer**: Custom **Enhanced Dot-Product Attention** over feature maps  
- **Classifier Head**:  
  - Linear → BatchNorm → ReLU → Dropout  
  - Layers of size 1024 → 512 → Num Classes (6)  

- **Loss Function**: Focal Loss (γ = 1.5) with class weights  
- **Optimizer**: AdamW  
- **Scheduler**: Cosine Annealing Warm Restarts  

---

## 📊 Results
- **Overall Test Accuracy**: **88.16%**  
- **Class-wise Performance**:

| Class       | Accuracy | Precision | Recall | F1-score |
|-------------|----------|-----------|--------|----------|
| Chickenpox  | 85.71%   | 75.00%    | 85.71% | 80.00%   |
| Cowpox      | 71.43%   | 83.33%    | 71.43% | 76.92%   |
| HFMD        | 93.75%   | 83.33%    | 93.75% | 88.24%   |
| Healthy     | 100.00%  | 100.00%   | 100.00%| 100.00%  |
| Measles     | 100.00%  | 66.67%    | 100.00%| 80.00%   |
| Monkeypox   | 82.76%   | 100.00%   | 82.76% | 90.57%   |

- **Best Validation Accuracy**: 90.07%  


