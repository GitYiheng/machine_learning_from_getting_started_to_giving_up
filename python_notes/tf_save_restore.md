# Save and Restore in TensorFlow

The savable/restorable paramters of the network are **Variables** (i.e. weights and biases).

To save and restore your variables, all you need to do is to call the `tf.train.Saver()` at the end of you graph.

```python
# create the graph
X = tf.placeholder(..)
Y = tf.placeholder(..)
w = tf.get_variale(..)
b = tf.get_variale(..)
...
loss = tf.losses.mean_squared_error(..)
optimizer = tf.train.AdamOptimizer(..).minimize(loss)
...

saver = tf.train.Saver()
```

In the **train mode**, in the session we will initialize the variables and run our network. At the end of training, we will save the variables using `saver.save()`:

```python
# TRAIN
with tf.Session() as sess:
    sess.run(tf.globale_variables_initializer())
    # train our model
    for step in range(steps):
        sess.run(optimizer)
        ...
    saved_path = saver.save(sess, './my-model', global_step=step)
```

This will create 3 files (data, index, meta) with a suffix of the step you saved your model.

In the **test mode**, in the session we will restore the variables using `saver.restore()` and validate or test our model.

# Save and Restore Two Variables:

## Save

We will start with saving and restoring two variables in TensorFlow. We will create a graph with two variables. Let's create two variables `a = [3, 3]` and `b = [5, 5, 5]`:

```python
import tensorflow as tf
# create variables a and b
a = tf.get_variable("A", initializer=tf.constant(3, shape=[2]))
b = tf.get_variable("B", initializer=tf.constant(5, shape=[3]))
```

Notice the **lower**case letter as python name and **UPPER**case letter as TensorFlow name. It will be important when we want to import the graph in restoring the data.

Variables need to be initialized before being used. To do so, we have to invoke a **variable initializer operation** and run the operation on the session. This is the easiest way to initialize variables which initializes all variables at once.

```python
# initialize all of the variables
init_op = tf.global_variables_initializer()
```

Now, on the session, we can initialize the variables and run them to see the values:

```python
# run the session
with tf.Session() as sess:
    # initialize all of the variables in the session
    sess.run(init_op)
    # run the session to get the value of the variable
    a_out, b_out = sess.run([a, b])
    print('a = ', a_out)
    print('b = ', b_out)
```

All of the variables exist in the scope of the session. So, after the session is closed, we will loose the variable.

In order to save the variable, we will call the saver function using `tf.train.Saver()` in our graph. This function will find all the variables in the graph. We can see the list of all variables in `_var_list`. Let's create a `saver` object and take a look at the `_var_list` in the object:

```python
# create saver object
saver = tf.train.Saver()
for i, var in enumerate(saver._var_list):
    print('Var {}: {}'.format(i, var))
```

So, our graph consists of two variables that listed above.

Now that the saver object is created in the graph, in the session, we can call the `saver.save()` function to save the variables in the disk. We have to pass the created session (`sess`) and the path to the file that we want to save the variables:

```python
# run the session
with tf.Session() as sess:
    # initialize all of the variables in the session
    sess.run(init_op)

    # save the variable in the disk
    saved_path = saver.save(sess, './saved_variable')
    print('model saved in {}'.format(saved_path))
```

If you check your working directory, you will notice that 3 new files have been created with the name `saved_variable` in them.

```python
import os
for file in os.listdir('.'):
    if 'saved_variable' in file:
        print(file)
```

```
saved_variable.data-00000-of-00001
saved_variable.meta
saved_variable.index
```

- **.data**: Contains variable values
- **.meta**: Contains graph structure
- **.index**: Identifies checkpoints

# Restore

Now that all the things that you need is saved in the disk, you can load your saved variables in the session using `saver.restore()`:

```python
# run the session
with tf.Session() as sess:
    # restore the saved vairable
    saver.restore(sess, './saved_variable')
    # print the loaded variable
    a_out, b_out = sess.run([a, b])
    print('a = ', a_out)
    print('b = ', b_out)
```

Notice that this time we did not initialize the variables in our session. Instead, we restored them from the disk.

In order to restore the parameters, the graph should be defined. Since we defined the graph in top, we didn't have a problem restoring the parameters. But what happens if we have not loaded the graph?

```python
# delete the current graph
tf.reset_default_graph()
try:
    with tf.Session() as sess:
        # restore the saved vairable
        saver.restore(sess, './saved_variable')
        # print the loaded variable
        a_out, b_out = sess.run([a, b])
        print('a = ', a_out)
        print('b = ', b_out)
except Exception as e:
    print(str(e))
```

We can define the graph in two ways.

## Define the graph from scratch and then run the session:

This way is simple if you have your graph. So, what you can do is to create the graph and then restore your variables:

```python
# delete the current graph
tf.reset_default_graph()

# create a new graph
# create variables a and b
a = tf.get_variable("A", initializer=tf.constant(3, shape=[2]))
b = tf.get_variable("B", initializer=tf.constant(5, shape=[3]))

# initialize all of the variables
init_op = tf.global_variables_initializer()# create the graph

# create saver object
saver = tf.train.Saver()

# run the session
with tf.Session() as sess:
    # restore the saved vairable
    saver.restore(sess, './saved_variable')
    # print the loaded variable
    a_out, b_out = sess.run([a, b])
    print('a = ', a_out)
    print('b = ', b_out)
```

## Restore the graph from `.meta` file:

When we save the variables, it creates a `.meta` file. This file contains the graph structure. Therefore, we can import the meta graph using `tf.train.import_meta_graph()` and restore the values of the graph. Let's import the graph and see all tensors in the graph:

```python
# delete the current graph
tf.reset_default_graph()

# import the graph from the file
imported_graph = tf.train.import_meta_graph('saved_variable.meta')

# list all the tensors in the graph
for tensor in tf.get_default_graph().get_operations():
    print(tensor.name)
```

We defined the python names with **lower**case letters and in TensorFlow names with **UPPER**case letters. You can see that what we have here are the UPPERcase letter variables. It means that tf.train.Saver() saves the variables with the TensorFlow name. Now that we have the imported graph, and we know that we are interested in A and B tensors, we can restore the parameters:

```python
# run the session
with tf.Session() as sess:
    # restore the saved vairable
    imported_graph.restore(sess, './saved_variable')
    # print the loaded variable
    a_out, b_out = sess.run(['A:0','B:0'])
    print('a = ', a_out)
    print('b = ', b_out)
```

Notice that in `sess.run()` we provided the TensorFlow name of the tensors `'A:0'` and `'B:0'` instead of `a` and `b`.


