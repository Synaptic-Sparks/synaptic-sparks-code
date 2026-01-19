
# xAI Project: Explainable AI & Model Diagnostics

This repository hosts a comprehensive Computer Vision project built on TensorFlow. It goes beyond simple image classification by integrating **Explainable AI (xAI)** techniques to audit model performance and understand the decision-making logic of deep neural networks.

## 🚀 1. Project Philosophy: Transparency in AI

Modern deep learning models are often "black boxes." This project aims to peel back the layers by answering three critical questions:

1. **What** did the model see? (Feature extraction)
2. **Where** did it look? (Grad-CAM heatmaps)
3. **Why** did it fail? (Error analysis & Calibration)

---

## 🏗️ 2. The Technical Pipeline

### A. Data Engineering & Augmentation

The project utilizes a 1.47GB subset of ImageNet. To prevent the model from simply "memorizing" the training data, we implement a **Stochastic Augmentation Pipeline**.

* **Mechanism**: Each image is randomly altered during every epoch (rotation, zoom, flip).
* **Benefit**: This forces the model to learn the *essential features* of an object (e.g., the shape of a bucket) rather than specific pixel locations or lighting conditions.

### B. Exploratory Feature Topology (PCA)

Before the first training step, we perform a "vibe check" on our data using **Principal Component Analysis (PCA)**.

* **The Process**: We pass images through a pre-trained **MobileNetV2** (acting as a feature extractor) and reduce the resulting high-dimensional tensors into a 2D plot.
* **Goal**: If classes (like "Hammer" and "Bucket") are already clustered separately in 2D space, the model will have an easier time learning. If they overlap heavily, we know to expect high confusion.

### C. Transfer Learning Strategy

We utilize **Transfer Learning** to leverage the "knowledge" of models trained on millions of images.

* **Backbones**: We benchmark **MobileNetV2** (optimized for speed/mobile) against **ResNet50** (optimized for depth and accuracy via residual connections).
* **Architecture**: We freeze the base layers to keep the pre-trained features and only train a custom "Head" consisting of Global Average Pooling, a Dense layer ( units), and Dropout () to prevent overfitting.

---

## 🔍 3. Explainable AI (xAI) Suite

### Grad-CAM: Visualizing Attention

We implement **Gradient-weighted Class Activation Mapping (Grad-CAM)**. This technique produces a heatmap that highlights the specific pixels that contributed most to the model's final prediction.

* **Interpretation**: If the model predicts "Dog" but the heatmap is glowing on the "Grass" in the background, we know the model has learned a "spurious correlation" rather than the actual object.

### Model Calibration & Confidence

We use **Calibration Curves** to measure the model's "self-awareness."

* **Overconfidence**: A common issue where a model predicts a class with 99.9% confidence but is actually wrong.
* **Ambiguity Audit**: The notebook programmatically identifies these "confident failures" for manual inspection, which is critical for safety-sensitive AI applications.

---

## 📊 4. Performance Metrics

| Tool | Purpose |
| --- | --- |
| **Normalized Confusion Matrix** | Identifies which specific classes are being swapped (e.g., Binder vs. Notebook). |
| **F1-Score Analysis** | A balanced metric that accounts for both Precision and Recall, especially on our "Hard" test set. |
| **Hard vs. Easy Grid** | A side-by-side visual comparison of images the model found trivial vs. those that caused low confidence. |

---

## 🛠️ 5. Getting Started

1. **Clone the Repository**:
```bash
git clone https://github.com/Synaptic-Sparks/synaptic-sparks-code.git

```


2. **Environment**: Open `xAI_Proj.ipynb` in **Google Colab**.
3. **Run All**: The notebook includes an automated `gdown` script that handles the 1.47GB dataset download and extraction for you.

---

## ⚖️ 6. License

This project is licensed under the **MIT License**.

```text
Copyright (c) 2024 Synaptic Sparks

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```
