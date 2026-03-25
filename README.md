# What Does an Autoencoder Remember?

## Investigating Latent Dimension and Quality of Reconstruction

This repository contains a tutorial and supporting notebook for exploring how **latent dimension** affects the behaviour of a **fully connected autoencoder** trained on **Fashion-MNIST**.

The project focuses on one central question:

> **How little information can an autoencoder compress into before it forgets too much to reconstruct anything useful?**

To answer that, five otherwise identical models are trained with latent dimensions **2, 8, 16, 32, and 64**, while keeping the rest of the architecture and training setup fixed. This makes the experiment a controlled comparison of bottleneck size and reconstruction quality.

---

## Repository Structure

```text
.
├── data/
├── figures/
├── notebook/
├── tutorial/
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```
---

## Project Overview

An autoencoder is a neural network that learns to compress an input into a lower-dimensional representation and then reconstruct the original input from that compressed code. In this tutorial, the bottleneck is treated as the main design choice under investigation.

The key idea is simple:

* a **smaller latent space** forces stronger compression
* a **larger latent space** preserves more information
* the best choice depends on whether you care more about **visualisation**, **compression**, or **reconstruction quality**

This project is designed as a teaching resource, so it combines explanation, code, figures, practical interpretation, accessibility notes, and ethical considerations.

---

## Dataset

The tutorial uses **Fashion-MNIST**, a benchmark dataset of **70,000 grayscale 28×28 images** across **10 clothing categories**, including items such as T-shirts, trousers, dresses, coats, sandals, sneakers, bags, and ankle boots.

Fashion-MNIST was chosen instead of standard MNIST because clothing images contain richer structure, texture, and silhouette variation, making reconstruction differences easier to observe.

---

## Model Architecture

The autoencoder used in this project is a **fully connected (dense) autoencoder** with symmetric encoder and decoder blocks:

`784 -> 256 -> 128 -> latent_dim -> 128 -> 256 -> 784`

**Activations**

* Hidden layers: `ReLU`
* Output layer: `Sigmoid`

**Training setup**

* Loss: `Mean Squared Error (MSE)`
* Optimiser: `Adam`
* Learning rate: `1e-3`
* Epochs: `15`

The only element changed across experiments is the latent dimension.

---

## Experiment Design

Five models are trained using the same architecture and hyperparameters, with latent dimensions:

* **2**
* **8**
* **16**
* **32**
* **64**

This controlled setup allows reconstruction performance to be attributed directly to bottleneck size rather than other modelling changes.

The notebook evaluates the models using:

* **MSE** for reconstruction error
* **SSIM** for perceptual image quality
* **visual reconstruction grids**
* **2D latent space visualisation**
* **latent space interpolation**
* an **elbow-style comparison** of compression vs performance

---

## Final Results

|Latent Dim|Compression Ratio|Final MSE|SSIM|Interpretation|
|-|-:|-:|-:|-|
|2|392.0:1|0.029981|0.5351|Severe over-compression|
|8|98.0:1|0.017517|0.6570|Large gain over dim=2|
|16|49.0:1|0.016119|0.6726|Best result in this run|
|32|24.5:1|0.016385|0.6666|Good reconstruction|
|64|12.2:1|0.016459|0.6642|Strong reconstruction, limited extra gain|

### Main findings

1. **Latent dimension 2 is too small** for good Fashion-MNIST reconstruction.
2. The **largest performance improvement** occurs between **2 and 8 dimensions**.
3. Gains become much smaller after **8 to 16 dimensions**, showing **diminishing returns**.
4. **Latent dimension 16** produced the best MSE and SSIM values in this experiment.
5. Even without labels during training, the **2D latent space shows emergent clustering** by clothing category.

---

## Practical Guidance

A useful takeaway from the tutorial is that the "best" latent dimension depends on the task:

* **2–3 dimensions**: useful for direct visualisation, but weak for reconstruction
* **8–16 dimensions**: strong balance between compression and quality
* **32–64 dimensions**: better reconstruction, but with weaker compression efficiency
* when improvements flatten out, use the **elbow point** rather than choosing the largest bottleneck by default

---

## Notebook Walkthrough

The notebook includes:

1. dependency setup and imports
2. Fashion-MNIST loading and preview
3. autoencoder definition
4. training loop for multiple latent dimensions
5. MSE comparison across models
6. SSIM evaluation
7. visual reconstruction comparison
8. 2D latent space visualisation
9. latent space interpolation
10. elbow analysis for selecting latent dimension
11. final summary and interpretation

---

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/owendiche-sys/Autoencoder-Latent-Dimension-Tutorial.git
cd Autoencoder-Latent-Dimension-Tutorial
```

### 2. Create and activate a virtual environment

**Windows (PowerShell)**

```powershell
py -3.12 -m venv .venv
.\\.venv\\Scripts\\Activate.ps1
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install torch torchvision matplotlib scikit-image numpy jupyter
```

### 4. Launch Jupyter

```bash
jupyter notebook
```

Then open:

```text
autoencoder_tutorial.ipynb
```

---

## Dependencies

Core packages used in the notebook:

* `torch`
* `torchvision`
* `numpy`
* `matplotlib`
* `scikit-image`
* `jupyter`

---

## Accessibility

This project was designed with accessibility in mind:

* latent space plots use **both colour and marker shape**
* figure captions are written to help readers interpret results without relying only on visuals
* code and tutorial formatting aim to remain readable in screen-reader-compatible formats

---

## Ethical Considerations

Although autoencoders are unsupervised, they are not neutral. The learned latent space can reflect biases present in the training data. In real-world applications, this matters because:

* underrepresented groups may be reconstructed or encoded less effectively
* anomaly detection systems built on biased latent spaces may incorrectly flag rare or underrepresented cases
* low reconstruction loss does not always mean the representation is suitable for high-stakes tasks

For that reason, autoencoders should be used carefully in areas such as healthcare, security, or finance.

---

## References

The tutorial draws on the following core sources:

* Cover, T.M. and Thomas, J.A. (2006). *Elements of Information Theory*. 2nd edn. Wiley-Interscience.
* Goodfellow, I., Bengio, Y. and Courville, A. (2016). *Deep Learning*. MIT Press.
* Hinton, G.E. and Salakhutdinov, R.R. (2006). “Reducing the dimensionality of data with neural networks.” *Science*, 313(5786), 504–507.
* Kingma, D.P. and Welling, M. (2014). *Auto-Encoding Variational Bayes*.
* Vincent, P. et al. (2010). “Stacked denoising autoencoders.” *Journal of Machine Learning Research*, 11, 3371–3408.
* Wang, Z. et al. (2004). “Image quality assessment: from error visibility to structural similarity.” *IEEE Transactions on Image Processing*, 13(4), 600–612.
* Xiao, H., Rasul, K. and Vollgraf, R. (2017). *Fashion-MNIST: a Novel Image Dataset for Benchmarking Machine Learning Algorithms*.
* PyTorch Documentation.

---

## Author

**Owen Nda Diche**  
---

## Licence

This repository should include a licence file so others know how they are allowed to use the code and tutorial materials.

