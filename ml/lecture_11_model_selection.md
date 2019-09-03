# Model Selection

## Make Sure Your Model is Optimally Tuned

Remember ERM

<a href="https://www.codecogs.com/eqnedit.php?latex=\min_{\mathbf{w}}&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;\underbrace{l_{(s)}&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i),&space;y_i)}_{Loss}&space;&plus;&space;\underbrace{\lambda&space;r&space;(w)}_{Regularizer}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\min_{\mathbf{w}}&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;\underbrace{l_{(s)}&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i),&space;y_i)}_{Loss}&space;&plus;&space;\underbrace{\lambda&space;r&space;(w)}_{Regularizer}" title="\min_{\mathbf{w}} \frac{1}{n} \sum_{i=1}^{n} \underbrace{l_{(s)} (h_{\mathbf{w}} (\mathbf{x}_i), y_i)}_{Loss} + \underbrace{\lambda r (w)}_{Regularizer}" /></a>

How should we set <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a> (regulates the bias/variance)?

### Overfitting and Underfitting

There are two equally problematic cases which can arise when learning a classifier on a data set: underfitting and overfitting, each of which relate to the degree to which the data in the training set is extrapolated to apply to unknown data:

**Underfitting**: The classifier learned on the training set is not expressive enough to even account for the data provided. In this case, both the training error and the test error will be high, as the classifier does not account for relevant information present in the training set.

**Overfitting**: The classifier learned on the training set is too specific, and cannot be used to accurately infer anything about unseen data. Although training error continues to decrease over time, test error will begin to increase again as the classifier begins to make decisions based patterns which exist only in the training set and not in the broader distribution.

### Identify the Sweet Spot

Divide data into training and validation portions. Train your algorithm on the "training" split and evaluate it on the "validation" split, for various value of <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a> (Typical value: <a href="https://www.codecogs.com/eqnedit.php?latex=10^{-5}&space;\enspace&space;10^{-4}&space;\enspace&space;10^{-3}&space;\enspace&space;10^{-2}&space;\enspace&space;10^{-1}&space;\enspace&space;10^{0}&space;\enspace&space;10^{1}&space;\enspace&space;10^{-2}&space;\ldots" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10^{-5}&space;\enspace&space;10^{-4}&space;\enspace&space;10^{-3}&space;\enspace&space;10^{-2}&space;\enspace&space;10^{-1}&space;\enspace&space;10^{0}&space;\enspace&space;10^{1}&space;\enspace&space;10^{-2}&space;\ldots" title="10^{-5} \enspace 10^{-4} \enspace 10^{-3} \enspace 10^{-2} \enspace 10^{-1} \enspace 10^{0} \enspace 10^{1} \enspace 10^{-2} \ldots" /></a>).

**k-fold cross validation**

Divide your training data into <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a> partitions. Train on <a href="https://www.codecogs.com/eqnedit.php?latex=k-1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k-1" title="k-1" /></a> of them and leave one out as validation set. Do this <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a> times (i.e. leave out every partition exactly once) and average the validation error across runs. This gives you a good estimate of the validation error (even with standard deviation). In the extreme case, you can have <a href="https://www.codecogs.com/eqnedit.php?latex=k=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k=n" title="k=n" /></a>, i.e. you only leave a single data point out (this is often referred to as LOOCV -- Leave One Out Cross Validation). LOOCV is important if your data set is small and cannot afford to leave out many data points for evaluation.

**Telescopic search**

Do two searches: 1st, find the best order of magnitude for <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a>; 2nd, do a more fine-grained search around the best <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a> found so far. For example, first you try <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda&space;=&space;0.01,&space;0.1,&space;1,&space;10,&space;100" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda&space;=&space;0.01,&space;0.1,&space;1,&space;10,&space;100" title="\lambda = 0.01, 0.1, 1, 10, 100" /></a>. It turns out <a href="https://www.codecogs.com/eqnedit.php?latex=10" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10" title="10" /></a> is the best performing value. Then you try out <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda&space;=&space;5,&space;10,&space;15,&space;20,&space;25,&space;\ldots,&space;95" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda&space;=&space;5,&space;10,&space;15,&space;20,&space;25,&space;\ldots,&space;95" title="\lambda = 5, 10, 15, 20, 25, \ldots, 95" /></a> to test values "around" <a href="https://www.codecogs.com/eqnedit.php?latex=10" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10" title="10" /></a>.

### Early Stopping

Stop your optimization after <a href="https://www.codecogs.com/eqnedit.php?latex=M&space;(\geq&space;0)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?M&space;(\geq&space;0)" title="M (\geq 0)" /></a> number of gradient steps, even if optimization has not converged yet.
