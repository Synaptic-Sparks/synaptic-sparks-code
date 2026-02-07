# xAI Project: Explainable AI & Model Diagnostics

This repository hosts a comprehensive Computer Vision project built on TensorFlow. It goes beyond simple image classification by integrating **Explainable AI (xAI)** techniques to audit model performance and bridge the **"Reality Gap"** between lab benchmarks and real-world deployment.

## 🚀 1. Project Philosophy: Transparency in AI

Modern deep learning models are often "black boxes." This project aims to peel back the layers by answering three critical questions:

1. **What** did the model see? (Feature extraction & PCA)
2. **Where** did it look? (Grad-CAM heatmaps)
3. **Why** did it fail? (Context bias & Calibration audit)

---

## 🏗️ 2. The Technical Pipeline

### A. Dataset & Augmentation (ImageNet-1K Subset)

We utilized a subset of **ImageNet-1K** containing 10 distinct classes, including **Remote control, Mouse, Keyboard, Wooden spoon, Coffee mug, and Mushroom**.

* **Scale**: 13,000 training images and 500 test images.
* **Stochastic Augmentation**: To prevent "memorization," we implemented rotation, horizontal flips, zoom, and brightness adjustments.
* **Resizing**: A critical step in our pipeline was **resizing all images to ** to meet the specific input requirements of the **MobileNetV2** architecture.

*Fig 1: Distribution of the 10 ImageNet-1K classes.*

### B. Three-Tier Evaluation Strategy

We performed a deep dive into model robustness across three stages:

1. **Validation Performance**: Standard accuracy check during training (~84%).
2. **Subset Test Performance**: Performance on the "unseen" ImageNet-1K test folders.
3. **The "Reality Check" (Custom Real-World Data)**: We introduced a completely independent real-world dataset.
* **Result**: We observed a **42% performance drop** (Accuracy fell to 41.8%).
* **Insight**: This "Reality Gap" showed that the model struggled significantly with real-world noise it hadn't encountered during training.



### C. Architecture Benchmark: MobileNetV2 vs. ResNet50

| Model | Architecture | Accuracy | Conclusion |
| --- | --- | --- | --- |
| **MobileNetV2** | Lightweight | **~84%** | Stable; best for this data volume. |
| **ResNet50** | Deep Residual | **~30%** | Failed to converge; too complex for this subset. |

---

## 🔍 3. Explainable AI (xAI) Suite

### Grad-CAM: Visualizing Attention & Background Bias

*Fig 2: Heatmaps showing model focus on objects vs. background textures.*

We used **Grad-CAM** to "debug" why the model failed the real-world stress test.

* **Discovery**: The model often ignored the object (e.g., the Remote Control) and focused on **background textures** like wood grain or metal grilles. This "Context Bias" was the primary reason for the drop in robustness.

### Model Calibration & "Confident Failures"

We audited the model's "self-awareness."

* **The Problem**: On hard real-world data, the model exhibited extreme **Overconfidence**, labeling items incorrectly (e.g., Keyboard  Mouse) with **96-100% confidence**.

---

## 🛠️ 4. Getting Started

1. **Clone the Repository**:

```bash
git clone https://github.com/Synaptic-Sparks/synaptic-sparks-code.git

```

2. **Environment**: Open `xAI_Proj.ipynb` in **Google Colab**.
3. **Data Access**: The notebook includes an automated `gdown` script for the 1.47GB dataset.

---

## 📬 5. Contact Information

* **Zeeshan Ahmed**
* Role: Lead Developer / Model Architecture
* GitHub: [github.com/ZeeshanAhmed](https://github.com/Zeeshan6948)


* **Muhammad Uzair Janjua**
* Role: Data Engineer / xAI Specialist
* GitHub: [github.com/UzairJanjua](https://github.com/uzairjanjua1)



---

## ⚖️ 6. License

This project is licensed under the **MIT License**.

```text
Copyright (c) 2026 Synaptic Sparks

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

```
