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

![mnist dataset](https://upload.wikimedia.org/wikipedia/commons/2/27/MnistExamples.png)

## Data dimension

Here, we specify the dimensions of the images which will be used in several places in the code below. Defining these variables makes it easier (compared with using hard-coded number all throughout the code) to modify them later. Ideally these would be inferred from the data that has been read, but here we will just write the numbers.

It's important to note that in a linear model, we have to flatten the input images into a vector. Here, each of the <a href="https://www.codecogs.com/eqnedit.php?latex=28\times&space;28" target="_blank"><img src="https://latex.codecogs.com/gif.latex?28\times&space;28" title="28\times 28" /></a> images are flattened into a <a href="https://www.codecogs.com/eqnedit.php?latex=1\times&space;784" target="_blank"><img src="https://latex.codecogs.com/gif.latex?1\times&space;784" title="1\times 784" /></a> vector.

```python
img_h = img_w = 28             # MNIST images are 28x28
img_size_flat = img_h * img_w  # 28x28=784, the total number of pixels
n_classes = 10                 # Number of classes, one class per digit
```

## Helper functions to load the MNIST data

In this section, we'll write the function which automatically loads the MNIST data and returns it in our desired shape and format.

Here, we'll simply write a function (`load_data`) which has two modes: **train** (which loads the training and validation images and their corresponding labels) and **test** (which loads the test images and their corresponding labels). You can replace this function to use your own dataset.

Other than a function for loading the images and corresponding labels, we define two more functions:

- `randomize`: which randomizes the order of images and their labels. This is important to make sure that the input images are sorted in a completely random order. Moreover, at the beginning of each epoch, we will re-randomize the order of data samples to make sure that the trained model is not sensitive to the order of data.

- `get_next_batch`: which only selects a few number of images determined by the batch_size variable (if you don't know why, read about Stochastic Gradient Method)

```python
def load_data(mode='train'):
    """
    Function to (download and) load the MNIST data
    :param mode: train or test
    :return: images and the corresponding labels
    """
    from tensorflow.examples.tutorials.mnist import input_data
    mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
    if mode == 'train':
        x_train, y_train, x_valid, y_valid = mnist.train.images, mnist.train.labels, \
                                             mnist.validation.images, mnist.validation.labels
        return x_train, y_train, x_valid, y_valid
    elif mode == 'test':
        x_test, y_test = mnist.test.images, mnist.test.labels
    return x_test, y_test


def randomize(x, y):
    """ Randomizes the order of data samples and their corresponding labels"""
    permutation = np.random.permutation(y.shape[0])
    shuffled_x = x[permutation, :]
    shuffled_y = y[permutation]
    return shuffled_x, shuffled_y


def get_next_batch(x, y, start, end):
    x_batch = x[start:end]
    y_batch = y[start:end]
    return x_batch, y_batch
```

## Load the data and display the sizes

Now we can use the defined helper function in `train` mode which loads the train and validation images and their corresponding labels. We'll also display their sizes:

```python
# Load MNIST data
x_train, y_train, x_valid, y_valid = load_data(mode='train')
print("Size of:")
print("- Training-set:\t\t{}".format(len(y_train)))
print("- Validation-set:\t{}".format(len(y_valid)))
```

To get a better sense of the data, let's checkout the shapes of the loaded arrays.

```python
print('x_train:\t{}'.format(x_train.shape))
print('y_train:\t{}'.format(y_train.shape))
print('x_train:\t{}'.format(x_valid.shape))
print('y_valid:\t{}'.format(y_valid.shape))
```

As you can see, `x_train` and `x_valid` arrays contain 55000 and 5000 flattened images (of size <a href="https://www.codecogs.com/eqnedit.php?latex=28\times&space;28=784" target="_blank"><img src="https://latex.codecogs.com/gif.latex?28\times&space;28=784" title="28\times 28=784" /></a> values). `y_train` and `y_valid` contain the corresponding labels of the images in the training and validation set respectively.

Based on the dimesnion of the arrays, for each image, we have 10 values as its label. Why? This technique is called **One-Hot Encoding**. This means the labels have been converted from a single number to a vector whose length equals the number of possible classes. All elements of the vector are zero except for the <a href="https://www.codecogs.com/eqnedit.php?latex=i^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i^{th}" title="i^{th}" /></a> element which is one and means the class is <a href="https://www.codecogs.com/eqnedit.php?latex=i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i" title="i" /></a>. For example, the One-Hot encoded labels for the first 5 images in the validation set are:

```python
y_valid[:5, :]
```

where the 10 values in each row represents the label assigned to that partiular image.

# Hyperparameters

Here, we have about 55,000 images in our training set. It takes a long time to calculate the gradient of the model using all these images. We therefore use **Stochastic Gradient Descent** which only uses a small batch of images in each iteration of the optimizer. Let's define some of the terms usually used in this context:

- `epoch`: one forward pass and one backward pass of all the training examples.
- `batch size`: the number of training examples in one forward/backward pass. The higher the batch size, the more memory space you'll need.
- `iteration`: one forward pass and one backward pass of one batch of images the training examples.

```python
# Hyper-parameters
epochs = 10             # Total number of training epochs
batch_size = 100        # Training batch size
display_freq = 100      # Frequency of displaying the training results
learning_rate = 0.001   # The optimization initial learning rate
```

Given the above definitions, each epoch consists of 55,000/100=550 iterations.

# Helper functions for creating the network

## Helper functions for creating new variables

We need to define two variables <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{W}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{W}" title="\mathbf{W}" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{b}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{b}" title="\mathbf{b}" /></a> to construt our linear model. These are generally called model parameters. We use **Tensorflow Variables** of proper size and initialization to define them.The following functions are written to be later used for generating the weight and bias variables of the desired shape:

```python
def weight_variable(shape):
    """
    Create a weight variable with appropriate initialization
    :param name: weight name
    :param shape: weight shape
    :return: initialized weight variable
    """
    initer = tf.truncated_normal_initializer(stddev=0.01)
    return tf.get_variable('W',
                           dtype=tf.float32,
                           shape=shape,
                           initializer=initer)


def bias_variable(shape):
    """
    Create a bias variable with appropriate initialization
    :param name: bias variable name
    :param shape: bias variable shape
    :return: initialized bias variable
    """
    initial = tf.constant(0., shape=shape, dtype=tf.float32)
    return tf.get_variable('b',
                           dtype=tf.float32,
                           initializer=initial)
```

# Create the network graph

Now that we have defined all the helped functions to create our model, we can create our network.

## Placeholders for the inputs (x) and corresponding labels (y)

First we need to define the proper tensors to feed in the input values to our model. Placeholder variable is the suitable choice for the input images and corresponding labels. This allows us to change the inputs (images and labels) to the TensorFlow graph.

```python
# Create the graph for the linear model
# Placeholders for inputs (x) and outputs(y)
x = tf.placeholder(tf.float32, shape=[None, img_size_flat], name='X')
y = tf.placeholder(tf.float32, shape=[None, n_classes], name='Y')
```

Placeholder `x` is defined for the images; its data-type is set to `float32` and the shape is set to `[None, img_size_flat]`, where None means that the tensor may hold an arbitrary number of images with each image being a vector of length `img_size_flat`.

Next we have `y` which is the placeholder variable for the true labels associated with the images that were input in the placeholder variable `x`. The shape of this placeholder variable is `[None, num_classes]` which means it may hold an arbitrary number of labels and each label is a vector of length `num_classes` which is 10 in this case.

## Create the model structure

After creating the proper input, we have to pass it to our model. Since we have a linear classifier, we will have <a href="https://www.codecogs.com/eqnedit.php?latex=output\_logits=\mathbf{W}&space;\cdot&space;\mathbf{x}&space;&plus;&space;\mathbf{b}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?output\_logits=\mathbf{W}&space;\cdot&space;\mathbf{x}&space;&plus;&space;\mathbf{b}" title="output\_logits=\mathbf{W} \cdot \mathbf{x} + \mathbf{b}" /></a> and we will use `tf.nn.softmax` to normalize the `output_logits` between 0 and 1 as probabilities (predictions) of samples.

```python
# Create weight matrix initialized randomely from N~(0, 0.01)
W = weight_variable(shape=[img_size_flat, n_classes])

# Create bias vector initialized as zero
b = bias_variable(shape=[n_classes])

output_logits = tf.matmul(x, W) + b
```

## Define the loss function, optimizer, accuracy, and predicted class

After creating the network, we have to calculate the `loss` and optimize it. Also, to evaluate our model, we have to calculate the `correct_prediction` and `accuracy`. We will also define `cls_prediction` to visualize our results.

## Initialize all variables

We have to invoke a variable initializer operation to initialize all variables.

```python
# Creating the op for initializing all variables
init = tf.global_variables_initializer()
```

# Train

After creating the graph, it is time to train our model. To train the model, we have to create a session and run the graph in our session.

```python
# Create an interactive session (to keep the session in the other cells)
sess = tf.InteractiveSession()
# Initialize all variables
sess.run(init)
# Number of training iterations in each epoch
num_tr_iter = int(len(y_train) / batch_size)
for epoch in range(epochs):
    print('Training epoch: {}'.format(epoch + 1))
    # Randomly shuffle the training data at the beginning of each epoch 
    x_train, y_train = randomize(x_train, y_train)
    for iteration in range(num_tr_iter):
        start = iteration * batch_size
        end = (iteration + 1) * batch_size
        x_batch, y_batch = get_next_batch(x_train, y_train, start, end)

        # Run optimization op (backprop)
        feed_dict_batch = {x: x_batch, y: y_batch}
        sess.run(optimizer, feed_dict=feed_dict_batch)

        if iteration % display_freq == 0:
            # Calculate and display the batch loss and accuracy
            loss_batch, acc_batch = sess.run([loss, accuracy],
                                             feed_dict=feed_dict_batch)

            print("iter {0:3d}:\t Loss={1:.2f},\tTraining Accuracy={2:.01%}".
                  format(iteration, loss_batch, acc_batch))

    # Run validation after every epoch
    feed_dict_valid = {x: x_valid[:1000], y: y_valid[:1000]}
    loss_valid, acc_valid = sess.run([loss, accuracy], feed_dict=feed_dict_valid)
    print('---------------------------------------------------------')
    print("Epoch: {0}, validation loss: {1:.2f}, validation accuracy: {2:.01%}".
          format(epoch + 1, loss_valid, acc_valid))
    print('---------------------------------------------------------')
```

# Test

After the training is done, we have to test our model to see how good it performs on a new dataset. There are multiple approaches to for this purpose. We will use two different methods.

## Accuracy

One way that we can evaluate our model is reporting the accuracy on the test set.

```python
# Test the network after training
# Accuracy
x_test, y_test = load_data(mode='test')
feed_dict_test = {x: x_test[:1000], y: y_test[:1000]}
loss_test, acc_test = sess.run([loss, accuracy], feed_dict=feed_dict_test)
print('---------------------------------------------------------')
print("Test loss: {0:.2f}, test accuracy: {1:.01%}".format(loss_test, acc_test))
print('---------------------------------------------------------')
```

## Plot some results

Another way to evaluate the model is to visualize the input and the model results and compare them with the true label of the input. This is advantages in numerous ways. For example, even if you get a decent accuracy, when you plot the results, you might see all the samples have been classified in one class. Another example is when you plot, you can have a rough idea on which examples your model failed. Let's define the helper functions to plot some correct and missclassified examples.

### Helper functions for plotting the results

```python
def plot_images(images, cls_true, cls_pred=None, title=None):
    """
    Create figure with 3x3 sub-plots.
    :param images: array of images to be plotted, (9, img_h*img_w)
    :param cls_true: corresponding true labels (9,)
    :param cls_pred: corresponding true labels (9,)
    """
    fig, axes = plt.subplots(3, 3, figsize=(9, 9))
    fig.subplots_adjust(hspace=0.3, wspace=0.3)
    for i, ax in enumerate(axes.flat):
        # Plot image.
        ax.imshow(images[i].reshape(28, 28), cmap='binary')

        # Show true and predicted classes.
        if cls_pred is None:
            ax_title = "True: {0}".format(cls_true[i])
        else:
            ax_title = "True: {0}, Pred: {1}".format(cls_true[i], cls_pred[i])

        ax.set_title(ax_title)

        # Remove ticks from the plot.
        ax.set_xticks([])
        ax.set_yticks([])

    if title:
        plt.suptitle(title, size=20)
    plt.show(block=False)


def plot_example_errors(images, cls_true, cls_pred, title=None):
    """
    Function for plotting examples of images that have been mis-classified
    :param images: array of all images, (#imgs, img_h*img_w)
    :param cls_true: corresponding true labels, (#imgs,)
    :param cls_pred: corresponding predicted labels, (#imgs,)
    """
    # Negate the boolean array.
    incorrect = np.logical_not(np.equal(cls_pred, cls_true))

    # Get the images from the test-set that have been
    # incorrectly classified.
    incorrect_images = images[incorrect]

    # Get the true and predicted classes for those images.
    cls_pred = cls_pred[incorrect]
    cls_true = cls_true[incorrect]

    # Plot the first 9 images.
    plot_images(images=incorrect_images[0:9],
                cls_true=cls_true[0:9],
                cls_pred=cls_pred[0:9],
                title=title)
```

### Visualize correct and missclassified examples

```python
# Plot some of the correct and misclassified examples
cls_pred = sess.run(cls_prediction, feed_dict=feed_dict_test)
cls_true = np.argmax(y_test[:1000], axis=1)
plot_images(x_test, cls_true, cls_pred, title='Correct Examples')
plot_example_errors(x_test[:1000], cls_true, cls_pred, title='Misclassified Examples')
plt.show()
```

After we finished, we have to close the session to free the memory.

```python
sess.close()
```

We could have also used:

```python
with tf.Session as sess:
    ...
```
