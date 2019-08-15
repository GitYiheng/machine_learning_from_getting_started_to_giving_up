# TensorBoard

TensorBoard is a visualization software that comes with any standard TensorFlow installation. In Google’s words: "The computations you'll use TensorFlow for (like training a massive deep neural network) can be complex and confusing. To make it easier to understand, debug, and optimize TensorFlow programs, we've included a suite of visualization tools called TensorBoard."

# Visualizing the Graph

To make our TensorFlow program TensorBoard-activated, we need to add a very few lines of code to it. This will export the TensorFlow operations into a file, called **event file** (or event log file). TensorBoard is able to read this file and give insight into the model graph and its performance.

### Example 1

Let's create two constants and add them together. Constant tensors can be defined simply by defining their value:

```python
import tensorflow as tf

# create graph
a = tf.constant(2)
b = tf.constant(3)
c = tf.add(a, b)
# launch the graph in a session
with tf.Session() as sess:
    print(sess.run(c))
```

To visualize the program with TensorBoard, we need to write log files of the program. To write event files, we first need to create a **writer** for those logs, using this code:

```python
writer = tf.summary.FileWriter([logdir], [graph])
```

where **[logdir]** is the folder where you want to store those log files. You can choose [logdir] to be something meaningful such as './graphs'. The second argument **[graph]** is the graph of the program we're working on. There are two ways to get the graph:

1. Call the graph using `tf.get_default_graph()`, which returns the default graph of the program
2. Set it as `sess.graph` which returns the session's graph (note that this requires us to already have created a session).

We'll show both ways in the following example; however, the second way is more common. Either way, make sure to create a writer only after you’ve defined your graph. Otherwise, the graph visualized on TensorBoard would be incomplete.

Let's add the writer to the first example and visualize the graph.

```python
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create graph
a = tf.constant(2)
b = tf.constant(3)
c = tf.add(a, b)

# creating the writer out of the session
# writer = tf.summary.FileWriter('./graphs', tf.get_default_graph())

# launch the graph in a session
with tf.Session() as sess:
    # or creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    print(sess.run(c))
```

Now if you run this code, it creates a directory inside your current directory (beside your Python code) which contains the **event file**.

Next, go to Terminal and make sure that the present working directory is the same as where you ran your Python code. Then run:

```
tensorboard --logdir="./graphs" --port 6006
```

This will generate a link for you. Copy and paste that link into your browser.

"Const" and "Const_1" in the graph correspond to a and b, and the node "Add" corresponds to c. The names we give them (a, b, and c) are just **Python-names** which are for us to access them when we write code. They mean nothing for the internal TensorFlow. To make TensorBoard understand the names of your ops, you have to explicitly name them.

Let's modify the code one more time and add the names:

```python
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create graph
a = tf.constant(2, name="a")
b = tf.constant(3, name="b")
c = tf.add(a, b, name="addition")

# creating the writer out of the session
# writer = tf.summary.FileWriter('./graphs', tf.get_default_graph())

# launch the graph in a session
with tf.Session() as sess:
    # or creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    print(sess.run(c))
```

If you run your code several times with the same [logdir], there will be multiple event files in your [logdir]. TF will show only the latest graph and display the warning of multiple event files. To get rid of the warning, delete the event files you no longer need or save them in different [logdir] folders.

# Writing Summaries to Visualize Learning

So far we only focused on how to visualize the graph in TensorBoard. In this second part, we are now going to use a special operation called **summary** to visualize the model parameters (like weights and biases of a neural network), metrics (like loss or accuracy value), and images (like input images to a network).

**Summary** is a special TensorBoard operation that takes in a regular tensor and outputs the summarized data to your disk (i.e. in the event file). Basically, there are three main types of summaries:

1. `tf.summary.scalar`: used to write a single scalar-valued tensor (like classificaion loss or accuracy value)

2. `tf.summary.histogram`: used to plot histogram of all the values of a non-scalar tensor (like weight or bias matrices of a neural network)

3. `tf.summary.image`: used to plot images (like input images of a network, or generated output images of an autoencoder or a GAN)

In the following sections, we'll go through each of the above summary types in more details.

## tf.summary.scalar

It's for writing the values of a scalar tensor that changes over time or iterations. In the case of neural networks (say a simple network for classification task), it's usually used to monitor the changes of loss function or classification accuracy.

### Example 2

Randomly pick 100 values from a standard Normal distribution, N(0, 1), and plot them one after the other.

One way to do so is to simply create a variable and initialize it from a normal distribution (with mean=0 and std=1), then run a for loop in the session and initialize it 100 times. The code will be as follows and the required steps to write the summary is explained in the code:

```python
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the scalar variable
x_scalar = tf.get_variable('x_scalar', shape=[], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ____step 1:____ create the scalar summary
first_summary = tf.summary.scalar(name='My_first_scalar_summary', tensor=x_scalar)

init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 2:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    for step in range(100):
        # loop over several initializations of the variable
        sess.run(init)
        # ____step 3:____ evaluate the scalar summary
        summary = sess.run(first_summary)
        # ____step 4:____ add the summary to the writer (i.e. to the event file)
        writer.add_summary(summary, step)
    print('Done with writing the scalar summary')
```

Let's pull up TensorBoard and checkout the result. Like before, you need to open terminal and type:

```
tensorboard --logdir="./graphs" --port 6006
```

where "./graphs" is the name of directory you saved the event file into. If you open TensorBoard, you'll see a new tab named **"scalars"** next to the earlier discussed **"graphs"** tab.

The plot panel came under "My_first_scalar_summary" name which we determined in our code. The x-axis and y-axis shows the 100 steps and the corresponding values (random values from a standard normal dist.) of the variable respectively.

## tf.summary.histogram

It's for plotting the histogram of the values of a non-scalar tensor. This gives us a view of how does the histogram (and the distribution) of the tensor values change over time or iterations. In the case of neural networks, it's commonly used to monitor the changes of weights and biases distributions. It's very useful in detecting irregular behavior of the network parameters (like when many of the weights shrink to almost zero or grow largely).

Now let's go back to our previous example and add a histogram summary to it.

### Example 3

Continue the previous example by adding a matrix of size 30x40, whose entries come from a standard normal distribution. Initialize this matrix 100 times and plot the distribution of its entries over time.

```python
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the variables
x_scalar = tf.get_variable('x_scalar', shape=[], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))
x_matrix = tf.get_variable('x_matrix', shape=[30, 40], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ____step 1:____ create the summaries
# A scalar summary for the scalar tensor
scalar_summary = tf.summary.scalar('My_scalar_summary', x_scalar)
# A histogram summary for the non-scalar (i.e. 2D or matrix) tensor
histogram_summary = tf.summary.histogram('My_histogram_summary', x_matrix)

init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 2:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    for step in range(100):
        # loop over several initializations of the variable
        sess.run(init)
        # ____step 3:____ evaluate the merged summaries
        summary1, summary2 = sess.run([scalar_summary, histogram_summary])
        # s____step 4:____ add the summary to the writer (i.e. to the event file) to write on the disc
        writer.add_summary(summary1, step)
        # repeat steps 4 for the histogram summary
        writer.add_summary(summary2, step)
    print('Done writing the summaries')
```

If you open TensorBoard in your browser, you'll find two new tabs added to the top menu: "Distributions" and "Histograms".

The "Distributions" tab contains a plot that shows the distribution of the values of the tensor (y-axis) through steps (x-axis). You might ask what are the light and dark colors?

The answer is that each line on the chart represents a percentile in the distribution over the data. For example, the bottom line (the very light one) shows how the minimum value has changed over time, and the line in the middle shows how the median has changed. Reading from top to bottom, the lines have the following meaning: [maximum, 93%, 84%, 69%, 50%, 31%, 16%, 7%, minimum]

These percentiles can also be viewed as standard deviation boundaries on a normal distribution: [maximum, μ+1.5σ, μ+σ, μ+0.5σ, μ, μ-0.5σ, μ-σ, μ-1.5σ, minimum] so that the colored regions, read from inside to outside, have widths [σ, 2σ, 3σ] respectively.

Similarly, in the histogram panel, each chart shows temporal "slices" of data, where each slice is a histogram of the tensor at a given step. It's organized with the oldest timestep in the back, and the most recent timestep in front.

You can easily monitor the values on the histograms at any step. Just move your cursor on the plot and see the x-y values on the histograms. You can also change the Histogram Mode from "offset" to "overlay" to see the histograms overlaid with one another.

As it was shown in the code, you need to run each summary (e.g. `sess.run([scalar_summary, histogram_summary])`) and then use your writer to write each of them on the disk. In practice, you might use tens and hundreds of such summaries to track different parameters in your model. This makes running and writing the summaries extremly inefficient. The way around it is to merge all summaries in your graph and run them at once inside your session. This can be done using `tf.summary.merge_all()` method. If we use it for Example 3, the code changes as follows:

```python
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the variables
x_scalar = tf.get_variable('x_scalar', shape=[], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))
x_matrix = tf.get_variable('x_matrix', shape=[30, 40], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ____step 1:____ create the summaries
# A scalar summary for the scalar tensor
scalar_summary = tf.summary.scalar('My_scalar_summary', x_scalar)
# A histogram summary for the non-scalar (i.e. 2D or matrix) tensor
histogram_summary = tf.summary.histogram('My_histogram_summary', x_matrix)

# ____step 2:____ merge all summaries
merged = tf.summary.merge_all()

init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 3:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    for step in range(100):
        # loop over several initializations of the variable
        sess.run(init)
        # ____step 4:____ evaluate the merged summaries
        summary = sess.run(merged)
        # ____step 5:____ add summary to the writer (i.e. to the event file) to write on the disc
        writer.add_summary(summary, step)
    print('Done writing the summaries')
```

## tf.summary.image

As its name shows, this type of summary is for writing and visualizing tensors as images. In the case of neural networks, this is usually used for tracking the images that are either fed to the network (say in each batch) or the images generated in the output (such as the reconstructed images in an autoencoder; or the fake images made by the generator model of a Generative Adverserial Network). However, in general, this can be used for plotting any tensor. For example, you can visualize a weight matrix of size 30x40 as an image of 30x40 pixels.

An image summary can be created like:

```python
tf.summary.image(name, tensor, max_outputs=3)
```

where **name** is the name for the generated node (i.e. operation), tensor is the desired tensor to be written as an image summary (we will talk about its shape shortly), and max_outputs is the maximum number of elements from **tensor** to generate images for. but... what does it mean?! It will be answered by knowing the shape of **tensor**.

The **tensor** that you feed to `tf.summary.image` must be a 4-D tensor of shape `[batch_size, height, width, channels]` where batch_size is the number of images in the batch, height and width determines the size of the image and channel is: 1: for Grayscale images. 3: for RGB (i.e. color) images. 4: for RGBA images (where A stands for alpha).

Let's look at a very simple example to get the idea.

### Example 4

Let's define two variables:

1. Of size 30x10 as 3 **grayscale** images of size 10x10
2. Of size 50x30 as 5 **color** images of size 10x10

and plot them as images in TensorBoard.

```python
import tensorflow as tf
tf.reset_default_graph()   # To clear the defined variables and operations of the previous cell

# create the variables
w_gs = tf.get_variable('W_Grayscale', shape=[30, 10], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))
w_c = tf.get_variable('W_Color', shape=[50, 30], initializer=tf.truncated_normal_initializer(mean=0, stddev=1))

# ___step 0:___ reshape it to 4D-tensors
w_gs_reshaped = tf.reshape(w_gs, (3, 10, 10, 1))
w_c_reshaped = tf.reshape(w_c, (5, 10, 10, 3))

# ____step 1:____ create the summaries
gs_summary = tf.summary.image('Grayscale', w_gs_reshaped)
c_summary = tf.summary.image('Color', w_c_reshaped, max_outputs=5)

# ____step 2:____ merge all summaries
merged = tf.summary.merge_all()

# create the op for initializing all variables
init = tf.global_variables_initializer()

# launch the graph in a session
with tf.Session() as sess:
    # ____step 3:____ creating the writer inside the session
    writer = tf.summary.FileWriter('./graphs', sess.graph)
    # initialize all variables
    sess.run(init)
    # ____step 4:____ evaluate the merged op to get the summaries
    summary = sess.run(merged)
    # ____step 5:____ add summary to the writer (i.e. to the event file) to write on the disc
    writer.add_summary(summary)
    print('Done writing the summaries')
```

Now you can see images by opening TensorBoard like before and switch to IMAGES tab.
