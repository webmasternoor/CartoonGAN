# 🖼️ CartoonGAN

A PyTorch implementation of **CartoonGAN**, a generative adversarial network designed to transform real-world photos into stylized cartoon images.

***

## 📚 Table of Contents

*   Introduction
*   Dataset Generation
*   Training on Google Colab
*   Data Loader
*   Model Definition
*   Loss Function
*   Optimizer
*   Transforming Local Images
*   Credits
*   Notes & Next Steps
*   References

***

## 🔰 Introduction

**CartoonGAN** converts real photos into cartoon-style images using a generative adversarial network trained on cartoon and real image datasets. The architecture uses a generator–discriminator framework along with edge-smoothed cartoon images to stabilize training.

***

## 📦 Dataset Generation

### Cartoon Images

A collection of cartoon artworks representing the target domain style.

### Edge-Smoothed Cartoon Images

Used to reduce noisy edges and stabilize generator training.

Process:

1.  Apply edge-preserving smoothing (e.g., bilateral filtering).
2.  Ensure input-output structure matches original cartoon dataset.

### Photo Images

A diverse set of natural images representing real-world scenes.

***

## 💾 Training on Google Colab

### Uploading Data

To train smoothly on Colab:

*   Upload datasets to Google Drive
*   Mount Drive in Colab
*   Set dataset paths accordingly

Example:

```python
from google.colab import drive
drive.mount('/content/drive')
```

***

## 📥 Data Loader

The data loader:

*   Reads cartoon images, edge-smoothed cartoon images, and real photos.
*   Applies preprocessing (resize, crop, normalization).
*   Loads data into batches for training.

***

## 🧠 Model Definition

### Padding

Used to preserve spatial dimensions during convolution.

### Stride

Defines downsampling behavior within generator and discriminator.

### Learnings

*   Appropriate normalization improves stability.
*   Residual blocks enhance expressive capability of the generator.

***

## ⚙️ Loss Function

### 1. Adversarial Loss

Drives generator to produce cartoon-like images indistinguishable from real cartoons.

### 2. Content Loss

Uses high-level VGG feature maps to preserve original photo structures.

### 3. Learnings

#### Loss Implementation

*   Combine adversarial loss with content loss for best results.
*   Balance of losses is controlled using a parameter.

#### Parameter **ω**

Used in multiple phases of training.

##### Training Rounds:

*   **Round 1:** Warm-up using content loss
*   **Round 2:** Introduce adversarial loss
*   **Round 3:** Fine-tune generator
*   **Round 4:** Stabilize model with full loss weights

***

## 🚀 Optimizer

*   **Adam** optimizer commonly used
*   Recommended settings:

```python
lr = 0.0002
beta1 = 0.5
beta2 = 0.999
```

***

## 🖼️ Transforming an Image from Local Filesystem

Once trained:

1.  Load generator model weights
2.  Pass image through generator
3.  Save or display cartoonized output

Example:

```python
output = generator(input_image)
save_image(output, "cartoonized.png")
```

***

## 🙏 Credits

CartoonGAN original paper:  
**Chen, Yijun; Liu, Ming-Yu; Liao, Yung-Yu; Kautz, Jan; Cheng, Ming-Hsuan.**  
*“CartoonGAN: Generative Adversarial Networks for Photo Cartoonization.”*

***

## 📌 Notes / Next Steps

*   Consider experimenting with additional cartoon styles.
*   Add model export for ONNX or TensorRT.
*   Build a web UI (Flask/React) for real-time cartoonization.

***

## 🔗 References

*   CartoonGAN paper
*   PyTorch documentation
*   Google Colab GPU guide

***
