# TNM112 – Deep Learning Project: Image Colorization

A deep learning project for the course **TNM112 (Linköping University)** that trains a
neural network to **colorize grayscale images**. The network takes a single-channel
grayscale image as input and tries to reconstruct the original RGB image.

## About the project

The project uses a **U-Net** (encoder–decoder with skip connections) trained on the
**CIFAR-10** dataset. Images are converted to grayscale and used as input, while the
original color images serve as the ground truth during training.

- **Framework:** TensorFlow / Keras
- **Dataset:** CIFAR-10 (32×32 RGB, loaded automatically via Keras)
- **Model:** Fully-convolutional U-Net
- **Loss functions compared:** MSE (L2) and MAE (L1)

## File structure

| File | Description |
|------|-------------|
| `Colorizer.ipynb` | Main notebook: data loading, model, training, evaluation and visualization |
| `*epochsMSE.png` / `*epochMSE.png` | Colorization results after different numbers of epochs (MSE loss) |
| `50epochsMAE.png` | Result with MAE loss after 50 epochs |
| `*_graph.png` | Loss curves (train/val) from training |

## Getting started

### Requirements

- Python 3.x
- TensorFlow
- NumPy
- Matplotlib

Install the dependencies:

```bash
pip install tensorflow numpy matplotlib
```

### Run the project

Open the notebook and run the cells from top to bottom:

```bash
jupyter notebook Colorizer.ipynb
```

CIFAR-10 is downloaded automatically the first time. No manual data download is needed.

## How it works

1. **Load data** – CIFAR-10 is fetched and normalized to the range [0, 1].
2. **Create input** – RGB images are converted to grayscale (1 channel).
3. **Build the model** – A U-Net with encoder, bottleneck and decoder.
4. **Train** – The model learns to map grayscale → color (default: 50 epochs, batch size 64).
5. **Evaluate** – The model is tested on the test set.
6. **Visualize** – Input, prediction and ground truth are shown side by side.

### Switching loss function

In the compilation step of the notebook you can switch between MSE and MAE by
commenting the respective `model.compile(...)` block in/out:

```python
loss="mse"   # L2 loss (default)
# loss="mae" # L1 loss
```

## Results

The result images show how colorization improves with more epochs. Each result is
displayed in three rows: **input (grayscale)**, **model prediction** and **ground truth**.

| Epochs | Loss | Result | Loss curve |
|--------|------|--------|------------|
| 1 | MSE | `1epochMSE.png` | – |
| 10 | MSE | `10epochsMSE.png` | `10epochsMSE_graph.png` |
| 20 | MSE | `20epochsMSE.png` | `20epochsMSE_graph.png` |
| 50 | MSE | `50epochsMSE.png` | `50epochsMSE_graph.png` |
| 50 | MAE | `50epochsMAE.png` | – |

## Possible improvements

- More epochs or a larger dataset for sharper colors
- Use the Lab color space instead of RGB (common in colorization)
- A deeper or wider U-Net

## Authors

Project for the course TNM112 – Deep Learning, Linköping University.
