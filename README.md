# Galaxy Morphology Classification

## Team Members

- **Maysam Asser** (202200276)
- **Jana Ahmed** (202201853)


---

## Table of Contents

1. [Problem Understanding](#problem-understanding)
2. [Methodology](#methodology)
3. [Preprocessing](#preprocessing)
4. [Model Architecture Implementation](#model-architecture-implementation)
5. [Training and Evaluation](#training-and-evaluation)
6. [Challenges](#challenges)
7. [Conclusion](#conclusion)

---

## 1. Problem Understanding

Classifying galaxies by their morphology is essential to understanding how galaxies form and evolve. Galaxies are categorized into three main types: spiral, elliptical, and irregular, each with unique features.

Currently, galaxy classification is often done manually, which is time-consuming. As telescopes collect more data, there is a need for faster and automated methods to classify galaxies.

In this project, we create a deep learning model that classifies galaxies based on their images. The model uses various techniques like rotation, shifting, zooming, flipping, shearing, and fill_mode to improve performance and reduce the reliance on large datasets.

---

## 2. Methodology

We followed the methodology outlined below to build and evaluate the galaxy morphology classifier:

- **Preprocessing the Data**
- **Building and Comparing Models**:
  - Simple CNN
  - Deep CNN 1
  - Deep CNN 2
  - VGG16
  - ResNet50
  - EfficientNetB0

---

## 3. Preprocessing the Data

1. **Loading Galaxy Images and Labels**:
   - We used the **astroNN** library to load the galaxy images and their corresponding labels.
   - Dataset: `galaxy10sdss` (a subset of the original `galaxy10` dataset, which was too large for our system).

2. **Data Splitting**:
   - The dataset was split into training and testing sets (80% training, 20% testing).

3. **Normalization**:
   - The pixel values of the images were normalized to a scale between 0 and 1.

4. **Resizing**:
   - All images were resized to 32x32 pixels to ensure consistency.

5. **Color Conversion**:
   - Grayscale images were converted to RGB format for compatibility with the model.

6. **Data Augmentation**:
   - Applied transformations to the images to augment the dataset:
     - Rotation
     - Shifting (horizontal and vertical)
     - Zooming
     - Shearing
     - Flipping (horizontal and vertical)

---

## 4. Model Architecture Implementation

### CNN Models

1. **Simple CNN**:
   - Convolutional layers to extract features.
   - MaxPooling layers to reduce dimensionality.
   - Dropout layers to avoid overfitting.
   - Dense layers for final classification.

   **Results**:
   - **Epoch 24/40**: accuracy: 85.27%, val_accuracy: 75.93%

2. **Deep CNN 1**:
   - Added more layers to capture more complex features.
   - Used **Adam** optimizer for better convergence.

   **Results**:
   - **Epoch 27/40**: accuracy: 86.26%, val_accuracy: 76.91%

3. **Deep CNN 2**:
   - Another deeper CNN model with further improvements.
   
   **Results**:
   - **Epoch 22/40**: accuracy: 86.41%, val_accuracy: 74.70%

### Transfer Learning Models

1. **VGG16** (Pre-trained on ImageNet):
   - Frozen pre-trained layers, added custom layers for galaxy classification.
   
   **Results**:
   - **Epoch 10/10**: accuracy: 47.25%, val_accuracy: 47.62%

2. **ResNet50** (Pre-trained on ImageNet):
   - Similar structure to VGG16 but with additional Dense layers.
   - Fine-tuning involved unfreezing the last 10 layers.

   **Results**:
   - **Epoch 10/10**: accuracy: 49.64%, val_accuracy: 35.18%

3. **EfficientNetB0** (Pre-trained):
   - Fine-tuned by unfreezing the last 10 layers.
   - Added custom Dense layers for classification.

   **Results**:
   - **Epoch 7/20**: accuracy: 31.90%, val_accuracy: 31.88%

---

## 5. Training and Evaluation

### Training the Models

- **CNN Models**:
  - Trained for up to 40 epochs with early stopping if accuracy didn’t improve for 5 consecutive epochs.
  - Data augmentation was used to enhance robustness.
  
- **Transfer Learning Models** (VGG16, ResNet50, EfficientNetB0):
  - Initially trained with frozen layers for 20 epochs.
  - Fine-tuned by unfreezing the last 10 layers for an additional 10 epochs with a lower learning rate (0.00001).

### Evaluating the Models

- Accuracy and loss were measured and visualized throughout the training process.
- Predictions were compared with the true labels to evaluate performance.
- Models were compared in terms of validation accuracy, loss, and the number of epochs.

---

## 6. Challenges

1. **Dataset Compatibility**:
   - Ensuring the dataset used was compatible with the processing power available. The `galaxy10sdss` dataset was used to avoid crashes that occurred with the higher-quality `galaxy10` dataset.
   
2. **Model Optimization**:
   - Testing different models to find the best-performing architecture for galaxy classification.

3. **Resource Management**:
   - Efficient resource usage on platforms like Google Colab to prevent crashes and optimize the training process.

---

## 7. Conclusion

This project demonstrated how deep learning techniques, such as Convolutional Neural Networks (CNNs) and Transfer Learning, can be used to classify galaxies based on their morphology, drastically reducing the time spent on manual classification.

We tested multiple models:
- Basic CNN models.
- Deeper CNN models.
- Transfer learning with pre-trained models (VGG16, ResNet50, EfficientNetB0).

Despite the challenges with limited resources and small datasets, the CNN models provided better performance than pre-trained models like VGG16 and ResNet50, especially for smaller datasets.

The project proved that deep learning can significantly improve galaxy morphology classification tasks while managing the limitations of available data and hardware.

