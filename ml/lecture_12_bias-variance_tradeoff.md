# Bias-Variance Tradeoff

As usual, we are given a dataset <a href="https://www.codecogs.com/eqnedit.php?latex=D&space;=&space;\{&space;(\mathbf{x}_1&space;,&space;y_1),&space;\ldots&space;,&space;(\mathbf{x}_n&space;,&space;y_n)&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D&space;=&space;\{&space;(\mathbf{x}_1&space;,&space;y_1),&space;\ldots&space;,&space;(\mathbf{x}_n&space;,&space;y_n)&space;\}" title="D = \{ (\mathbf{x}_1 , y_1), \ldots , (\mathbf{x}_n , y_n) \}" /></a>, drawn i.i.d. from some distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a>. We assume a regression setting, i.e. <a href="https://www.codecogs.com/eqnedit.php?latex=y&space;\in&space;\mathbb{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;\in&space;\mathbb{R}" title="y \in \mathbb{R}" /></a>. We will decompose the generalization error of a regressor into three rather interpretable terms. Before we do that, let us consider that for any given input <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> there might not exist a unique label <a href="https://www.codecogs.com/eqnedit.php?latex=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y" title="y" /></a>. For example, if your vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> describes features of house (e.g. number of bedrooms, square footage, ...) and the label <a href="https://www.codecogs.com/eqnedit.php?latex=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y" title="y" /></a> its price, you could imagine two houses with identical description selling for different prices. So for any given feature vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>, there is a distribution over possible labels. We therefore define the following, which will come in useful later on:

**Expected Label** (given <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}&space;\in&space;\mathbb{R}^d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}&space;\in&space;\mathbb{R}^d" title="\mathbf{x} \in \mathbb{R}^d" /></a>):

<a href="https://www.codecogs.com/eqnedit.php?latex=\bar{y}(\mathbf{x})&space;=&space;E_{y&space;\vert&space;\mathbf{x}}&space;[Y]&space;=&space;\int_y&space;y&space;\text{Pr}(y&space;\vert&space;\mathbf{x})&space;\partial&space;y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{y}(\mathbf{x})&space;=&space;E_{y&space;\vert&space;\mathbf{x}}&space;[Y]&space;=&space;\int_y&space;y&space;\text{Pr}(y&space;\vert&space;\mathbf{x})&space;\partial&space;y" title="\bar{y}(\mathbf{x}) = E_{y \vert \mathbf{x}} [Y] = \int_y y \text{Pr}(y \vert \mathbf{x}) \partial y" /></a>.

The expected label denotes the label you would expect to obtain, given a feature vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>. So we draw our training set <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a>, consisting of <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> inputs, i.i.d. from the distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P" title="P" /></a>. As a second step we typically call some machine learning algorithm <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{A}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{A}" title="\mathcal{A}" /></a> on this dataset to learn a hypothesis (a.k.a. classifier). Formally, we denote this process as <a href="https://www.codecogs.com/eqnedit.php?latex=h_D&space;=&space;\mathcal{A}(D)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_D&space;=&space;\mathcal{A}(D)" title="h_D = \mathcal{A}(D)" /></a>.

For a given <a href="https://www.codecogs.com/eqnedit.php?latex=h_D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_D" title="h_D" /></a>, learned on dataset <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a> with algorithm <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{A}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{A}" title="\mathcal{A}" /></a>, we can compute the generalization error (as measured in squared loss) as follows:

**Expected Test Error** (given <a href="https://www.codecogs.com/eqnedit.php?latex=h_D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_D" title="h_D" /></a>):

<a href="https://www.codecogs.com/eqnedit.php?latex=E_{(\mathbf{x},&space;y)&space;\sim&space;P}&space;[(h_D&space;(\mathbf{x})&space;-&space;y))^2]&space;=&space;\int_x&space;\int_y&space;(h_D&space;(\mathbf{x})&space;-&space;y)^2&space;\text{Pr}&space;(\mathbf{x},&space;y)&space;\partial&space;y&space;\partial&space;\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_{(\mathbf{x},&space;y)&space;\sim&space;P}&space;[(h_D&space;(\mathbf{x})&space;-&space;y))^2]&space;=&space;\int_x&space;\int_y&space;(h_D&space;(\mathbf{x})&space;-&space;y)^2&space;\text{Pr}&space;(\mathbf{x},&space;y)&space;\partial&space;y&space;\partial&space;\mathbf{x}" title="E_{(\mathbf{x}, y) \sim P} [(h_D (\mathbf{x}) - y))^2] = \int_x \int_y (h_D (\mathbf{x}) - y)^2 \text{Pr} (\mathbf{x}, y) \partial y \partial \mathbf{x}" /></a>

Note that one can use other loss functions. We use squared loss because it has nice mathematical properties, and it is also the most common loss function.

The previous statement is true for a given training set <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a>. However, remember that <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a> itself is drawn from <a href="https://www.codecogs.com/eqnedit.php?latex=P^n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P^n" title="P^n" /></a>, and is therefore a random variable. Further, <a href="https://www.codecogs.com/eqnedit.php?latex=h_D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_D" title="h_D" /></a> is a function of <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a>, and is therefore also a random variable. And we can of course compute its expectation:

**Expected Classifier** (given <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{A}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{A}" title="\mathcal{A}" /></a>):

<a href="https://www.codecogs.com/eqnedit.php?latex=\bar{h}&space;=&space;E_{D&space;\sim&space;P^n}&space;[h_D]&space;=&space;\int_D&space;h_D&space;\text{Pr}&space;(D)&space;\partial&space;D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{h}&space;=&space;E_{D&space;\sim&space;P^n}&space;[h_D]&space;=&space;\int_D&space;h_D&space;\text{Pr}&space;(D)&space;\partial&space;D" title="\bar{h} = E_{D \sim P^n} [h_D] = \int_D h_D \text{Pr} (D) \partial D" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\text{Pr}(D)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\text{Pr}(D)" title="\text{Pr}(D)" /></a> is the probability of drawing <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a> from <a href="https://www.codecogs.com/eqnedit.php?latex=P^n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P^n" title="P^n" /></a>. Here, <a href="https://www.codecogs.com/eqnedit.php?latex=\bar{h}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{h}" title="\bar{h}" /></a> is a weighted average over functions.

We can also use the fact that <a href="https://www.codecogs.com/eqnedit.php?latex=h_D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_D" title="h_D" /></a> is a random variable to compute the expected test error only given <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{A}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{A}" title="\mathcal{A}" /></a>, taking the expectation also over <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a>.

**Expected Test Error** (given <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{A}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{A}" title="\mathcal{A}" /></a>):

<a href="https://www.codecogs.com/eqnedit.php?latex=E_{(\mathbf{x},&space;y)&space;\sim&space;P,\,&space;D&space;\sim&space;P^n}&space;[(h_D&space;(\mathbf{x})&space;-&space;y)^2]&space;=&space;\int_D&space;\int_\mathbf{x}&space;\int_y&space;(h_D&space;(\mathbf{x})&space;-&space;y)^2&space;P&space;(\mathbf{x},&space;y)&space;P(D)&space;\partial&space;\mathbf{x}&space;\partial&space;y&space;\partial&space;D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_{(\mathbf{x},&space;y)&space;\sim&space;P,\,&space;D&space;\sim&space;P^n}&space;[(h_D&space;(\mathbf{x})&space;-&space;y)^2]&space;=&space;\int_D&space;\int_\mathbf{x}&space;\int_y&space;(h_D&space;(\mathbf{x})&space;-&space;y)^2&space;P&space;(\mathbf{x},&space;y)&space;P(D)&space;\partial&space;\mathbf{x}&space;\partial&space;y&space;\partial&space;D" title="E_{(\mathbf{x}, y) \sim P,\, D \sim P^n} [(h_D (\mathbf{x}) - y)^2] = \int_D \int_\mathbf{x} \int_y (h_D (\mathbf{x}) - y)^2 P (\mathbf{x}, y) P(D) \partial \mathbf{x} \partial y \partial D" /></a>

To be clear, <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a> is our training point and the <a href="https://www.codecogs.com/eqnedit.php?latex=(\mathbf{x},&space;y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\mathbf{x},&space;y)" title="(\mathbf{x}, y)" /></a> pairs are the test points. We are interested in exactly this expression, because it evaluates the quality of a machine learning algorithm <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{A}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{A}" title="\mathcal{A}" /></a> with respect to a data distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a>. In the following we will show that this expression decomposes into three meaningful terms.































