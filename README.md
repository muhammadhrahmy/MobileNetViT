# MobileNetViT: Lightweight Hybrid CNN-ViT for Brain Tumor Classification with Explainability

**A lightweight hybrid CNN-Vision Transformer architecture achieving 99.16% accuracy with only 2.99M parameters for brain tumor MRI classification.**

---

## 🎯 Overview

MobileNetViT combines the efficiency of MobileNetV2's convolutional backbone with Vision Transformer's global attention mechanisms through **dual-stream token processing**, enabling state-of-the-art diagnostic performance in resource constrained clinical environments.

### Key Features

- ✅ **99.16% Classification Accuracy** — Highest among evaluated architectures
- ✅ **2.99M Parameters** — Lightest model (11.52 MB storage, 103.27 MB GPU memory)
- ✅ **Real-Time Inference** — 6.78ms model inference (147 FPS)
- ✅ **Integrated Explainability** — Optimized Score-CAM visualization (75.23ms total, 13 FPS)
- ✅ **Two Phase Training** — Strategic frozen backbone + fine tuning (+1.98% improvement)
- ✅ **Resource Efficient** — Deployable on edge devices and low resource clinical settings

---

## 📊 Dataset

This project uses the **Brain Tumor MRI Dataset** from Kaggle:

**Dataset Link:** [Brain Tumor MRI Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset/versions/1)

### Dataset Statistics

| Split | Images | Classes |
|-------|--------|---------|
| **Training** | 22,850 (5× augmented) | 4 |
| **Validation** | 1,142 | 4 |
| **Test** | 1,311 | 4 |

**Tumor Categories:**
- Glioma (300 test samples)
- Meningioma (306 test samples)
- No Tumor (405 test samples)
- Pituitary (300 test samples)

---

## 🏗️ Architecture

MobileNetViT employs a **dual-stream hybrid design**:

1. **MobileNetV2 Backbone** — Efficient depthwise separable convolutions for local feature extraction
2. **Patch Embedding** — Converts spatial features to token representations (49 patches → 7×7 grid)
3. **Dual-Stream Processing:**
   - **Local CNN Pathway** — 24 tokens processed via depthwise convolutions (preserves translation invariance)
   - **Global Transformer Pathway** — 25 tokens processed via multi head self attention (captures long range dependencies)
4. **Fusion Module** — Combines complementary local + global features
5. **Classification Head** — 4 class softmax output

### Model Specifications

| Metric | Value |
|--------|-------|
| Parameters | 2.99M |
| Model Size | 11.52 MB |
| FLOPs | 0.35G |
| Inference Time | 6.78 ± 0.57 ms |
| GPU Memory | 103.27 MB |
| Throughput | 147 FPS (model only), 13 FPS (with Score-CAM) |

---

## 📁 Repository Structure
- EDA: Exploratory data analysis and dataset statistics
- Pre Processing: Image preprocessing and augmentation pipelines
- Benchmarking: Baseline model implementations and evaluation scripts
- Proposed Models: MobileNetViT and EfficientNetViT architectures
- Explainability: Optimized Score-CAM visualization implementation
- Inferencing: Inference scripts

---

## 📈 Results

### Classification Performance

| Model | Accuracy | Parameters | Size | FLOPs | Inference Time |
|-------|----------|------------|------|-------|----------------|
| **MobileNetViT** | **99.16%** | **2.99M** | **11.52 MB** | **0.35G** | **6.78 ms** |
| EfficientNetViT | 98.78% | 4.12M | 15.89 MB | 0.42G | 8.23 ms |
| TinyViT-5M | 98.86% | 5.40M | 20.82 MB | 1.30G | 12.45 ms |
| ResNet50 | 98.47% | 23.59M | 90.97 MB | 4.11G | 18.34 ms |
| ViT-Base | 98.17% | 85.80M | 330.95 MB | 17.58G | 45.67 ms |

### Per-Class Performance (MobileNetViT)

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
| Glioma | 98.67% | 98.67% | 98.67% | 300 |
| Meningioma | 99.35% | 99.35% | 99.35% | 306 |
| No Tumor | 99.01% | 99.26% | 99.13% | 405 |
| Pituitary | 99.67% | 99.67% | 99.67% | 300 |
| **Overall** | **99.16%** | **99.16%** | **99.16%** | **1,311** |

### Score-CAM Explainability

- **Pituitary Tumors:** Excellent localization (sharply focused on sellar region)
- **Meningioma:** Good localization (highlights dural attachment)
- **No Tumor:** Diffuse patterns (expected for normal scans)
- **Glioma:** Challenging (reflects infiltrative tumor characteristics)

**Computational Efficiency:**
- Model inference: 6.78 ± 0.57 ms
- Score-CAM overhead: 68.44 ± 0.96 ms
- **Total system time: 75.23 ± 1.41 ms (13.29 FPS)**

---
