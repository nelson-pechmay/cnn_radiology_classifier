# cnn_radiology_classifier

This repository is meant to show a basic Deep Learning based classifier for chest X-Rays. It classifies chest X-Ray images into COVID19, Pneumonia, or a healthy lung (Normal).

# Description

This repository contains two main files:

1. RadiologyAI_nelsonpm.ipynb
2. report_project03_nelson.pdf

The first one, is a jupyter notebook and contains all code used for this project. It is based on the starter code provided by course Computer Vision II - Applications at opencv. The second one, is a detailed report in pdf of the code employed for this project. That's a simple guide through the notebook.

## The model

Briefly, I have chosen the VGG16 model as the starting architecture. This is one of the most *classical* CNN (convolutional neural-network) architectures, which was awarded the first prize in the ImageNet competition in 2014 [(VGG16 paper)](https://arxiv.org/abs/1409.1556). *Transfer learning* was used on the provided dataset, by freezen all convolutional layers of the VGG16, except for the last six, which where retrained. On top of this, a 2D global max pooling was added, followed by a fully-connected layer of 512 nodes (using `ReLu` as ativation function), then a dropout of 50 % was added (for regularization) and finally a 3 node output layer with `softmax` activation for the classification of the three labelled classes in the dataset: normal, pneumonia or covid19.
The model was trained on 11290 training images and 3215 validation images. The resulting model was tested on 1563 test images. The notebook was runned on the google colab platform.

# Sample results

Even though the trained model shows slight overfitting, the obtained performance on the test dataset looks promising, as readed from the precision, recall and f1-score metrics:

|             | precision | recall | f1-score | support |
|-------------|-----------|--------|----------|---------|
|          0  |    0.99   |  0.99  |   0.99   |   491|
|          1  |    0.95   |  0.99  |   0.97   |   545|
|          2  |    1.00   |  0.96  |   0.98   |   527|
|-------------|-----------|--------|----------|---------|
|   accuracy  |           |        |   0.98   |  1563|
|  macro avg  |    0.98   |  0.98  |   0.98   |  1563|
|weighted avg |    0.98   |  0.98  |   0.98   |  1563|

On the classification report above, the image labels are encoded by numbers: 0-covid19, 1-normal, 2-pneumonia. However, the confusion matrix (without noramlization) can help better to visualize the number of miss-classified cases on the test dataset. For example, 21 were classified with "pneoumonia", when they were actually "normal". That is, around 4 % from a sample of 1563, as can be readed from the normalized confusion matrix.


