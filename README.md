# **Image Classification CNN Model**

## Overview
Convolutional Neural Network (CNN), also known as ConvNet, is a specialized type of deep learning algorithm mainly designed for tasks that necessitate object recognition, including image classification, detection, and segmentation. 

This project uses a Convolutional Neural Network (CNN) to classify images of **cats** and **dogs**.
It trains on labeled image data, tracks performance metrics during training, and visualizes accuracy and loss over time.

---

## Dataset Setup

1. **Kaggle API Authentication**

   * Create a hidden directory `.kaggle` in your home folder.
   * Copy `kaggle.json` (Kaggle API credentials) into `.kaggle/`.
   * Authenticate using the Kaggle API.
2. **Dataset Download**

   * Use the Kaggle CLI to download the dataset (e.g., `owner/dataset-name`).
   * Downloaded as `dogs-vs-cats.zip` into `/content/`.
3. **Extraction**

   * Unzip using Python’s `zipfile` module.
   * Organize images into `/content/train/dog/` and `/content/train/cat/`.

---

## Data Loading in TensorFlow

The training and validation datasets are created using TensorFlow’s **`image_dataset_from_directory()`** method, which allows efficient loading of images directly from a directory structure.

**Parameters used:**

* **`directory`** = `'/content/train'`
  Path to the root training directory. Images are stored in subfolders by class:

  ```
  /content/train/cat/
  /content/train/dog/
  ```

* **`labels`** = `'inferred'`
  Labels are automatically assigned based on the subfolder names (`cat` → 0, `dog` → 1).

* **`label_mode`** = `'int'`
  Labels are returned as integers, which is optimal for binary classification with `binary_crossentropy`.

* **`batch_size`** = `32`
  Loads 32 images at a time, improving training efficiency and reducing memory load.

* **`image_size`** = `(256, 256)`
  All images are resized to a uniform size for consistent input shape to the CNN.As we have different sized images.

---

## Data Preprocessing 

Image preprocessing is done **before feeding data to the CNN** to improve learning stability and model performance.

1. **Normalization**

   * Pixel values are originally in the range **0–255** (uint8 format).
   * They are scaled to the range **0–1** by dividing by 255.0.
   * This prevents large input values from causing unstable gradient updates.

2. **Label Encoding**

   * Since we use binary classification, labels remain as integers (0 for cat, 1 for dog), directly compatible with the loss function.


---

## CNN Model Architecture

* **3× Convolutional Layers** + **MaxPooling Layers**
* **Flatten Layer**
* **Dense Layer** (output)
* **Summary** 
<img width="857" height="625" alt="image" src="https://github.com/user-attachments/assets/928fcbeb-35bd-4f84-b866-14c67c1872be" />


---

## Compilation & Training

1. **Compile**

   * Optimizer: `'adam'` (adaptive learning rate)
   * Loss: `'binary_crossentropy'` (binary classification)
   * Metrics: `['accuracy']`
2. **Train**

   * Training dataset: 20,000 images
   * Epochs: `10`
   * Validation dataset used after each epoch (no weight updates).

---

## Results & Observations

* Initial model shows **overfitting**:

  * High training accuracy
  * Low validation accuracy
  <img width="747" height="545" alt="image" src="https://github.com/user-attachments/assets/a13ae9b1-cef5-4c01-b825-eda14a9406c6" />
  
  * Loss output graphs
  <img width="700" height="533" alt="image" src="https://github.com/user-attachments/assets/c2059eca-1cff-4519-82de-82df8e3ecdf7" />


---

## Overfitting Reduction

* Added **Batch Normalization** and **Dropout** layers.
* Retrained model — gap between training and validation performance reduced.
* Further improvements possible with **L1/L2 Regularization**.

<img width="723" height="527" alt="image" src="https://github.com/user-attachments/assets/0eead747-0d6b-46f8-a760-07eb1e8c534c" />


---

## Key Takeaways

* CNNs can effectively classify cats vs dogs with sufficient preprocessing.
* Proper regularization techniques help control overfitting.
* Model performance can be improved by experimenting with architecture and hyperparameters.

---
