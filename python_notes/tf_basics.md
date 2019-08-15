# Computational Graphs

A computational graph is an abstract way of describing computations as a directed graph. A directed graph is a data structure consisting of nodes (vertices) and edges. It’s a set of vertices connected pairwise by directed edges.

TensorFlow uses directed graphs internally to represent computations, and they call this data flow graphs (or computational graphs).

While nodes in a directed graph can be anything, nodes in a computational graph mostly represent **operations**, **variables**, or **placeholders**.

The edges correspond to data, or multidimensional arrays (so-called Tensors) that flow through the different operations. In other words, edges carry information from one node to another. The output of one operation (one node) becomes the input to another operation and the edge connecting the two nodes carry the value.

# TensorFlow Basics

A computational graph in TensorFlow consists of several parts:

- **Variables**: Think of TensorFlow variables like normal variables in our computer programs. A variable can be modified at any point in time, but the difference is that they have to be initialized before running the graph in a session. They represent **changeable parameters** within the graph. A good example for variables would be the weights or biases in a neural network.

- **Placeholders**: A placeholder allows us to feed data into the graph from outside and unlike variables they don’t need to be initialized. Placeholders simply define the shape and the data type. We can think of placeholders as **empty nodes** in the graph where the value is provided later on. They are typically used for feeding in inputs and labels.

- **Constants**: Parameters that cannot be changed.

- **Operations**: Operations represent nodes in the graph that perform computations on Tensors.

- **Graph**: A graph is like a central hub that connects all the variables, placeholders, constants to operations.

- **Session**: A session creates a runtime in which operations are executed and Tensors are evaluated. It also allocates memory and holds the values of intermediate results and variables.

TensorFlow is composed of **Graph** and **Session**. The Graph class is used to construct the computational graph and the Session is used to execute and evaluate all or a subset of nodes. The main advantage of deferred execution is that during the definition of the computational graph we can construct very complex expressions without directly evaluating them and allocating the space in memory that is needed.

With those core building blocks, a program can be divided into two phases:

1. Construction of the computational graph.

2. Running a session

# Graph

A **Graph** contains a set of **Operation** objects, which represent units of computation. In addition, a graph contains a set of **Placeholder** and **Variable** objects, which represent the units of data that flow between operations.

For our implementation we essentially need three lists to store all those objects. Furthermore, our graph needs a method called **as_default** which we can call to create a **global variable** that is used to store the current graph instance. This way, we don’t have to pass around the reference to the graph when creating operations, placeholders or variables.

```python
class Graph():
    def __init__(self):
        self.operations = []
        self.placeholders = []
        self.variables = []
        self.constants = []

    def as_default(self):
        global _default_graph
        _default_graph = self
```

# Operations

Operations are the nodes in the computational graph and perform computations on Tensors. Most operations take zero or many Tensors as input, and produce zero or more Tensors objects as output.

In a nutshell, an operation is characterized as follows:

1. It has a list of input_nodes
2. Implement a forward function
3. Implement a backward function
4. Remember its output
5. Add itself to the default graph

Each node is only aware of its immediate surrounding, meaning it knows about its local inputs coming in and its output that is directly being passed on to the next node that is consuming it.

```python
class Operation():
    def __init__(self, input_nodes=None):
        self.input_nodes = input_nodes
        self.output = None

        # Append operation to the list of operations of the default graph
        _default_graph.operations.append(self)

    def forward(self):
        pass

    def backward(self):
        pass
```

# Placeholder

In TensorFlow there are different ways for providing input values to the graph, such as **Placeholder**, **Variable** or **Constant**.

```python
class Placeholder():
    def __init__(self):
        self.value = None
        _default_graph.placeholders.append(self)
```

# Constant

Constants are quite the opposite of variables as they cannot be changed once initialized. Variables on the other hand, represent changeable parameters in our computational graph. For example, the weights and biases in a neural network.

It definitely makes sense to use placeholders for the inputs and labels rather than variables, as they always change per iteration. Also, the distinction is very important as variables are being optimized during the backward pass while constants and placeholders are not. So we cannot just simply use a variable for feeding in constant. A placeholder would work, but that also feels a bit misused. To provide such feature, we introduce constants.

```python
class Constant():
    def __init__(self, value=None):
        self.__value = value
        _default_graph.constants.append(self)

    @property
    def value(self):
        return self.__value

    @value.setter
    def value(self, value):
        raise ValueError("Cannot reassign value.")
```

# Variable

Variables require initial values and append themselves to the default graph.

```python
class Variable():
    def __init__(self, initial_value=None):
        self.value = initial_value
        _default_graph.variables.append(self)
```

# Session

From TensorFlow we know that a **session** has a **run** method

```python
session = Session()
output = session.run(some_operation, {
    X: train_X # [1,2,...,n_features]
})
```

So **run** takes two parameters, an **operation** to be executed and a dictionary **feed_dict** that maps graph elements to values. This dictionary is used to feed in values for the placeholders in our graph. The operation that is provided is a graph element that we want to compute an output for.



