# Softmax vs Sigmoid

The sigmoid function is used for the two-class case, whereas the softmax function is used for the multiclass case.

Sigmoid is equivalent to softmax in the two-class case (binary classification), however in case of multinomial classification, sigmoid allows to deal with non-exclusive labels (multi-labels), while softmax deals with exclusive classes (one-hot encoded).

In the two-class case, the predicted probablies are as follows, using the sigmoid function:

<a href="https://www.codecogs.com/eqnedit.php?latex=Pr(Y_i=0)=\frac{e^{-\beta\cdot&space;X_i}}{1&plus;e^{-\beta\cdot&space;X_i}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Pr(Y_i=0)=\frac{e^{-\beta\cdot&space;X_i}}{1&plus;e^{-\beta\cdot&space;X_i}}" title="Pr(Y_i=0)=\frac{e^{-\beta\cdot X_i}}{1+e^{-\beta\cdot X_i}}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=Pr(Y_i=1)=1-Pr(Y_i=0)=\frac{1}{1&plus;e^{-\beta\cdot&space;X_i}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Pr(Y_i=1)=1-Pr(Y_i=0)=\frac{1}{1&plus;e^{-\beta\cdot&space;X_i}}" title="Pr(Y_i=1)=1-Pr(Y_i=0)=\frac{1}{1+e^{-\beta\cdot X_i}}" /></a>

Choosing a larger base value e<sup>-&beta;</sup>>0 will create a probability distribution that is more concentrated around the positions of the largest input values.

In the multiclass case, with K classes, the predicted probabilities are as follows, using the softmax function:

<a href="https://www.codecogs.com/eqnedit.php?latex=Pr(Y_i=k)=\frac{e^{-\beta\cdot&space;X_i}}{\sum_{j=1}^{K}&space;e^{-\beta\cdot&space;X_j}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Pr(Y_i=k)=\frac{e^{-\beta\cdot&space;X_i}}{\sum_{j=1}^{K}&space;e^{-\beta\cdot&space;X_j}}" title="Pr(Y_i=k)=\frac{e^{-\beta\cdot X_i}}{\sum_{j=1}^{K} e^{-\beta\cdot X_j}}" /></a>

# What is a Logit

A logit (also called a score) is a raw unscaled value associated with a class, before computing the probability. In terms of neural network architecture, this means that a logit is an output of a dense (fully-connected) layer.
