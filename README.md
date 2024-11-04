# Generative Adversarial Networks

This repository contains code for training a Generative Adversarial Network (GAN) using TensorFlow to generate images of cars based on the Stanford Cars Dataset.  The architecture consists of a Generator and a Discriminator neural network that are trained adversarially. 
 The Generator learns to create realistic car images, while the Discriminator learns to distinguish between real images from the dataset and fake images produced by the Generator.  Eventually, the Generator produces such high quality fake images that our Discriminator model can no longer tell if the output is from its dataset or fake.  At that point, it only ever outputs a 1/2 probability in determining if it's real or fake.

# Prerequisites
Ensure you have the following libraries installed:

- Python 3.7 or later
- TensorFlow 2.x
- DeepLake

Other Python libraries:
- NumPy
- Matplotlib

# Dataset
The notebook utilizes the Stanford Cars Dataset accessed via DeepLake.

# Code Structure
# Data Loading and Preprocessing
- Loads the Stanford Cars Dataset from DeepLake
- Preprocesses images: resizing to (240, 360), normalizez pixel values to [-1, 1]

# Generator Network
- Defines a Generator model using tf.keras layers
- The Generator takes a noise vector and produces a generated car image

# Discriminator Network
- Defines a Discriminator model to classify images as real or fake
- Uses convolutional layers to extract features from images

# Training Loop
- Implements the training process with adversarial training of both networks
- Saves model checkpoints and outputs generated images at intervals

# Utilities
- Functions for generating and displaying images
- Checkpoint management in the event of runtime disconnects

# Training and Hyperparameters
- BATCH_SIZE: 128
- BUFFER_SIZE: 8000
- EPOCHS: 800
- noise_dim: 100
- IMAGE_SAVE_INTERVAL: 100 epochs
- Feel free to adjust these parameters to your liking.  You may want to experiment using a lower batch size (e.g. 32) and buffer size (e.g. 1000) if you don't have the hardware to support it due to the resolution of the Stanford cars dataset.  You still want to have enough variability in there so your generated images don't start having too similar of features.  You may also start with a lower epoch threshold as these models do take a long time to train

# Optimizer Settings
- Uses the Adam optimizer with a learning rate of 1e-4 and beta_1 of 0.5
- You may want to experiment with different learning rates (e.g. the default 1e-3) until you find a good convergence point

# Loss Functions
- Binary cross-entropy loss is used for both our networks
- Label smoothing is applied to the real labels in the Discriminator loss
- We use label smoothing to prevent our Discriminator model from being too good at its predictions, which can result in less reliable when it comes to any new unseen data

# Checkpoints
- Model checkpoints are saved every 100 epochs to the ./training_checkpoints_cars_deeplake directory

# Usage
- You can install the DeepLake libraries as follows:
   ```sh
   pip install deeplake
- You'll also need to install this other DeepLake library as follows:
   ```sh
   pip install "deeplake<4"
