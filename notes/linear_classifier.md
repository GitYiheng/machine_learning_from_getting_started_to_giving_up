# Linear Classifier by Logistic Regression

Technically, in a linear model we will use the simplest function to predict the label <a href="https://www.codecogs.com/eqnedit.php?latex=y_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i" title="y_i" /></a> of the image <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a>. We'll do so by using a linear mapping like <a href="https://www.codecogs.com/eqnedit.php?latex=f(\mathbf{x}_i,&space;\mathbf{W},&space;\mathbf{b})=\mathbf{W}&space;\mathbf{x}_i&space;&plus;&space;\mathbf{b}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f(\mathbf{x}_i,&space;\mathbf{W},&space;\mathbf{b})=\mathbf{W}&space;\mathbf{x}_i&space;&plus;&space;\mathbf{b}" title="f(\mathbf{x}_i, \mathbf{W}, \mathbf{b})=\mathbf{W} \mathbf{x}_i + \mathbf{b}" /></a> where <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{W}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{W}" title="\mathbf{W}" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{b}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{b}" title="\mathbf{b}" /></a> are called weight matrix and bias vector respectively.

# Import the required libraries:

We will start with importing the required Python libraries.

```python
# imports
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
```

# Load the MNIST data

MNIST is a dataset of handwritten digits. If you are into machine learning, you might have heard of this dataset by now. MNIST is kind of benchmark of datasets for deep learning and is easily accesible through Tensorflow

The dataset contains 55,000 examples for training, 5,000 examples for validation and 10,000 examples for testing. The digits have been size-normalized and centered in a fixed-size image (<a href="https://www.codecogs.com/eqnedit.php?latex=28\times&space;28" target="_blank"><img src="https://latex.codecogs.com/gif.latex?28\times&space;28" title="28\times 28" /></a> pixels) with values from 0 to 1. For simplicity, each image has been flattened and converted to a 1-D numpy array of 784 features (<a href="https://www.codecogs.com/eqnedit.php?latex=28\times&space;28" target="_blank"><img src="https://latex.codecogs.com/gif.latex?28\times&space;28" title="28\times 28" /></a>).

![alt text](https://en.wikipedia.org/wiki/MNIST_database#/media/File:MnistExamples.png "mnist dataset")
