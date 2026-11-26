# Food-101 Image Classifier using CNN

This project teaches a computer to look at a photo of food and tell which dish it is. For example, you show it a picture, and it says "pizza" or "tacos".

It is built with Python, TensorFlow and Keras, and it runs on Google Colab.

---

## What is this project about?

Image classification means giving a computer a picture and asking, "What is in this picture?"

In this project, the computer learns from 101,000 food photos. After learning, it tries to name the food in photos it has never seen before.

---

## Dataset

- **Name:** Food-101
- **Total images:** 101,000
- **Food types (classes):** 101 (pizza, tacos, sushi, burgers, and more)
- **Images per food:** about 1,000
- **Download link:** https://d3ilbtxij3aepc.cloudfront.net/projects/CNN-PROJECT-1-6/food-101.zip

The images come in different sizes, so all of them were resized to 224 x 224 pixels.

**How the data was split:**

| Part | Images | Purpose |
|---|---|---|
| Training (80%) | 80,800 | The model learns from these |
| Validation (20%) | 20,200 | Used to test the model on new photos |

---

## Tools Used

- Python
- TensorFlow and Keras (to build and train the model)
- NumPy (for numbers)
- Matplotlib (for images and graphs)
- Pillow / PIL (to read image sizes)
- Google Colab (to run the code online)

---

## How the Project Works (Step by Step)

1. **Download and unzip** the Food-101 dataset. Each food has its own folder.
2. **Look at sample images** to understand the data. The images have different sizes.
3. **Load the data** with batch size 32 and image size 224 x 224. Split it 80% training and 20% validation.
4. **Scale the pixels.** Pixel values go from 0-255 down to 0-1, which helps the model learn better.
5. **Build the CNN model** (details below).
6. **Train the model** for 25 rounds (called epochs).
7. **Save the model** as `food_classifier.keras`.
8. **Plot a graph** of training accuracy vs. validation accuracy.

---

## Model Details

The model is a Convolutional Neural Network (CNN). A CNN is a type of model that is very good at understanding images. It first finds small patterns like edges and colors, then bigger patterns like shapes and textures, and finally decides what the food is.

| Layer | What it does |
|---|---|
| Conv2D (32 filters) + BatchNorm + MaxPool | Finds simple patterns like edges |
| Conv2D (64 filters) + BatchNorm + MaxPool | Finds slightly bigger patterns |
| Conv2D (128 filters) + BatchNorm + MaxPool | Finds shapes and textures |
| Conv2D (256 filters) + BatchNorm + MaxPool | Finds complex food features |
| Global Average Pooling | Makes a short summary of all patterns |
| Dense (512) | Makes the decision |
| Dropout (0.5) | Stops the model from just memorizing |
| Dense (101, Softmax) | Gives a score for each of the 101 foods |

- **Total parameters:** about 573,000 (2.19 MB)
- **Optimizer:** Adam
- **Loss function:** Sparse Categorical Crossentropy
- **Metric:** Accuracy
- **Epochs:** 25

---

## Results

| Measure | Result |
|---|---|
| Training accuracy | about 74% |
| Validation accuracy | about 47% to 49% |
| Best validation point | around epoch 8 |

- Training accuracy kept going up in all 25 epochs.
- Validation accuracy went up until about epoch 8, then stayed flat.

---

## What Do the Results Mean?

The model is **overfitting**.

Think of a student who memorizes last year's exam answers. They score very high on those exact questions, but they struggle when new questions come. Our model did the same thing. It learned the training photos very well, but it is only about 48% correct on new photos.

Still, 48% is not bad for this task. If the model guessed randomly among 101 foods, it would be right only about 1% of the time. So the model did learn real food features.

**Why did this happen?**

- The model was trained from scratch, with no earlier knowledge.
- No data augmentation was used, so it saw the same images again and again.
- Training continued after epoch 8 even though it stopped improving.
- Many foods look alike (for example, different pasta dishes or steaks).

---

## Limitations

- Accuracy on new images is only about 48%.
- The model overfits.
- No data augmentation was used.
- No confusion matrix was made, so we do not know which foods get mixed up.

---

## How to Improve It

1. **Transfer learning:** Use a ready-made model like MobileNetV2, EfficientNet or ResNet. This is the biggest improvement and can give about 70% to 85% accuracy.
2. **Data augmentation:** Flip, rotate and zoom the images so the model sees more variety.
3. **Early stopping:** Stop training automatically when validation accuracy stops improving.
4. **Regularization (L2):** Reduce memorizing.
5. **Learning rate scheduler:** Make training smoother.
6. **Hyperparameter tuning:** Try different batch sizes, learning rates and dropout values.
7. **Confusion matrix:** See which foods the model mixes up.

---

## How to Run This Project

1. Download the dataset from the link above.
2. Upload `food-101.zip` to your Google Drive.
3. Open `food_classification.ipynb` in Google Colab.
4. Update the zip file path in the unzip cell if your path is different.
5. Run all the cells from top to bottom.
6. The trained model will be saved as `food_classifier.keras`.

---

## Conclusion

This project builds a CNN from scratch that can classify 101 types of food from photos. The model reaches about 74% accuracy on training images and about 48% on new images, which shows overfitting.

The project covers the full deep learning process: loading data, preparing it, building a model, training it, saving it and checking the results. The next step is to use transfer learning and data augmentation to get much better accuracy.