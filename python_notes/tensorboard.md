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



