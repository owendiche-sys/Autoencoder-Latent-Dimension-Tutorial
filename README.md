 # What Does an Autoencoder Remember?

## Exploring Latent Dimension and Reconstruction Quality

This repository contains the code, figures, and PDF tutorial for a machine learning assignment on **autoencoders**. The project investigates how the size of the **latent dimension** affects the reconstruction quality of a **fully connected autoencoder** trained on the **Fashion-MNIST** dataset.

The central question of the tutorial is:

**How much information can a fully connected autoencoder compress before reconstruction quality begins to break down?**

## Project overview

An autoencoder is a neural network that learns to reconstruct its input by passing it through a compressed internal representation called the **latent space** or **bottleneck**. In this project, the bottleneck size is varied to study how compression strength affects reconstruction performance.

Five latent dimensions were tested:

- 2
- 8
- 16
- 32
- 64

The results show that very small bottlenecks lead to noticeably worse reconstructions, while moderate latent dimensions preserve much more useful visual information.

## Repository structure



```text

autoencoder-latent-dimension-tutorial/
│
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
│
├── tutorial/
│   └── autoencoder\_latent\_dimension\_tutorial.pdf
│
├── notebooks/
│   └── autoencoder\_latent\_dimension\_tutorial.ipynb
│
├── figures/
│   ├── figure1\_reconstruction\_loss.png
│   ├── figure2\_loss\_curves.png
│   ├── figure3\_reconstructions.png
│   └── figure4\_latent\_space.png
│
└── data/
    └── README.md

```


## Dataset


This project uses Fashion-MNIST, a dataset of 28 × 28 grayscale images of clothing items such as shirts, shoes, coats, and bags.

The dataset is downloaded automatically in the notebook using torchvision.datasets.FashionMNIST, so no manual download is required.


## Method summary

A fully connected autoencoder was implemented in PyTorch. The encoder compresses each 28 × 28 image into a lower-dimensional latent vector, and the decoder reconstructs the image from that vector.

## Architecture



&nbsp;- Input: 784

&nbsp;- Hidden layers: 256, 128

&nbsp;- Latent dimensions tested: 2, 8, 16, 32, 64

&nbsp;- Decoder mirrors the encoder

&nbsp;- Output activation: Sigmoid

## Training setup



&nbsp;- Loss function: Mean Squared Error (MSE)

&nbsp;- Optimiser: Adam

&nbsp;- Epochs: 15

&nbsp;- Dataset: Fashion-MNIST subset

&nbsp;- Framework: PyTorch


## Key findings



&nbsp;- A latent dimension of 2 compressed the images too aggressively and produced the highest reconstruction loss.

&nbsp;- Latent dimensions 8, 16, 32, and 64 performed much better.

&nbsp;- 32 achieved the lowest final test reconstruction loss in this experiment.

&nbsp;- The improvement after moderate latent sizes became smaller, suggesting diminishing returns.



## How to run the project

This project was developed in Google Colab.

## Option 1: Run in Google Colab
Upload or open the notebook in Google Colab, then run all cells from top to bottom:

notebooks/autoencoder\_latent\_dimension\_tutorial.ipynb

The Fashion-MNIST dataset will be downloaded automatically during execution.

## Option 2: Run locally
Clone the repository:

```bash
git clone https://github.com/your-username/autoencoder-latent-dimension-tutorial.git

cd autoencoder-latent-dimension-tutorial
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Then open the notebook in Jupyter Notebook or JupyterLab and run all cells from top to bottom.

## Requirements

Main packages used:

&nbsp;- torch

&nbsp;- torchvision

&nbsp;- matplotlib

&nbsp;- numpy

&nbsp;- pandas

&nbsp;- scikit-learn

&nbsp;- jupyter


See requirements.txt for the full list.

## Tutorial output
The notebook reproduces:

&nbsp;- reconstruction loss comparison across latent dimensions

&nbsp;- test loss curves

&nbsp;- original vs reconstructed images

&nbsp;- 2D latent space visualisation

&nbsp;- summary table of final test losses


## Accessibility considerations
&nbsp;- This project was designed to remain easy to follow by:

&nbsp;- using clear section headings

&nbsp;- labelling figures clearly

&nbsp;- comparing a small number of latent dimensions

&nbsp;- including side-by-side image reconstructions

&nbsp;- avoiding reliance on colour alone to communicate the main findings


## References

Goodfellow, I., Bengio, Y. and Courville, A. (2016) Deep Learning. Cambridge, MA: MIT Press.

Hinton, G.E. and Salakhutdinov, R.R. (2006) ‘Reducing the dimensionality of data with neural networks’, Science, 313(5786), pp. 504–507.

PyTorch Documentation (n.d.) PyTorch 2.x documentation.

Vincent, P., Larochelle, H., Lajoie, I., Bengio, Y. and Manzagol, P.-A. (2010) ‘Stacked denoising autoencoders: Learning useful representations in a deep network with a local denoising criterion’, Journal of Machine Learning Research, 11, pp. 3371–3408.

Xiao, H., Rasul, K. and Vollgraf, R. (2017) Fashion-MNIST: a Novel Image Dataset for Benchmarking Machine Learning Algorithms. arXiv:1708.07747.



