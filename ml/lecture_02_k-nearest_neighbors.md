# K-Nearest Neighbors

## The K-NN Algorithm

*Assumption*: Similar inputs have similar outputs.

*Classification rule*: For a test input <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>, assign the most common label amongst its <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a> most similar training inputs.

*Formal (and borderline incomprehensible) definition of k-NN*:

- Test point: <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>
- Denote the set of the <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a> nearest neighbors of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> as <a href="https://www.codecogs.com/eqnedit.php?latex=S_{\mathbf{x}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{\mathbf{x}}" title="S_{\mathbf{x}}" /></a>. Formally <a href="https://www.codecogs.com/eqnedit.php?latex=S_{\mathbf{x}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{\mathbf{x}}" title="S_{\mathbf{x}}" /></a> is defined as <a href="https://www.codecogs.com/eqnedit.php?latex=S_{\mathbf{x}}&space;\subseteq&space;D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{\mathbf{x}}&space;\subseteq&space;D" title="S_{\mathbf{x}} \subseteq D" /></a> s.t. <a href="https://www.codecogs.com/eqnedit.php?latex=\vert&space;S_{\mathbf{x}}&space;\vert&space;=&space;k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\vert&space;S_{\mathbf{x}}&space;\vert&space;=&space;k" title="\vert S_{\mathbf{x}} \vert = k" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\forall(\mathbf{x}',&space;y')&space;\in&space;D&space;\backslash&space;S_{\mathbf{x}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\forall(\mathbf{x}',&space;y')&space;\in&space;D&space;\backslash&space;S_{\mathbf{x}}" title="\forall(\mathbf{x}', y') \in D \backslash S_{\mathbf{x}}" /></a>,

<a href="https://www.codecogs.com/eqnedit.php?latex=dist(\mathbf{x},&space;\mathbf{x}')&space;\geq&space;\max_{(\mathbf{x}'',&space;y'')&space;\in&space;S_{\mathbf{x}}}&space;dist(\mathbf{x},&space;\mathbf{x}'')" target="_blank"><img src="https://latex.codecogs.com/gif.latex?dist(\mathbf{x},&space;\mathbf{x}')&space;\geq&space;\max_{(\mathbf{x}'',&space;y'')&space;\in&space;S_{\mathbf{x}}}&space;dist(\mathbf{x},&space;\mathbf{x}'')" title="dist(\mathbf{x}, \mathbf{x}') \geq \max_{(\mathbf{x}'', y'') \in S_{\mathbf{x}}} dist(\mathbf{x}, \mathbf{x}'')" /></a>,

(i.e. every point in <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a> but *not* in <a href="https://www.codecogs.com/eqnedit.php?latex=S_{\mathbf{x}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{\mathbf{x}}" title="S_{\mathbf{x}}" /></a> is at least as far away from <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> as furthest point in <a href="https://www.codecogs.com/eqnedit.php?latex=S_{\mathbf{x}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{\mathbf{x}}" title="S_{\mathbf{x}}" /></a>). We can then define the classifier <a href="https://www.codecogs.com/eqnedit.php?latex=h()" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h()" title="h()" /></a> as a function returning the most common label in <a href="https://www.codecogs.com/eqnedit.php?latex=S_{\mathbf{x}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{\mathbf{x}}" title="S_{\mathbf{x}}" /></a>:

<a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x})&space;=&space;mode(\{&space;y'':&space;(\mathbf{x}'',&space;y'')&space;\in&space;S_{\mathbf{x}}&space;\})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x})&space;=&space;mode(\{&space;y'':&space;(\mathbf{x}'',&space;y'')&space;\in&space;S_{\mathbf{x}}&space;\})" title="h(\mathbf{x}) = mode(\{ y'': (\mathbf{x}'', y'') \in S_{\mathbf{x}} \})" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=mode(\cdot)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?mode(\cdot)" title="mode(\cdot)" /></a> means to select the label of the highest occurence.

## What Distance Function Should We Use?

The k-nearest neighbor classifier fundamentally relies on a distance metric. The better that metric reflects label similarity, the better the classified will be. The most common choice is the **Minkowski distance**

<a href="https://www.codecogs.com/eqnedit.php?latex=dist(\mathbf{x},&space;\mathbf{z})&space;=&space;\Big(&space;\sum_{r=1}^{d}&space;\vert&space;x_r&space;-&space;z_r&space;\vert^p&space;\Big)^{1/p}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?dist(\mathbf{x},&space;\mathbf{z})&space;=&space;\Big(&space;\sum_{r=1}^{d}&space;\vert&space;x_r&space;-&space;z_r&space;\vert^p&space;\Big)^{1/p}" title="dist(\mathbf{x}, \mathbf{z}) = \Big( \sum_{r=1}^{d} \vert x_r - z_r \vert^p \Big)^{1/p}" /></a>.

## Brief Digression (Bayes Optimal Classifier)

**Example**: Assume (and this is almost never the case) you knew <a href="https://www.codecogs.com/eqnedit.php?latex=P(y&space;\vert&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y&space;\vert&space;\mathbf{x})" title="P(y \vert \mathbf{x})" /></a>, then you would simply predict the most likely label.

The Bayes optimal classifier predicts: <a href="https://www.codecogs.com/eqnedit.php?latex=y^{\ast}&space;=&space;h_{opt}(\mathbf{x})&space;=&space;\operatorname*{argmax}_{y}&space;P(y&space;\vert&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y^{\ast}&space;=&space;h_{opt}(\mathbf{x})&space;=&space;\operatorname*{argmax}_{y}&space;P(y&space;\vert&space;\mathbf{x})" title="y^{\ast} = h_{opt}(\mathbf{x}) = \operatorname*{argmax}_{y} P(y \vert \mathbf{x})" /></a>

Although the Bayes optimal classifier is as good as it gets, it still can make mistakes. It is always wrong if a sample does not have the most likely label. We can compute the probability of that happening precisely (which is exactly the error rate):

<a href="https://www.codecogs.com/eqnedit.php?latex=\epsilon_{BayesOpt}&space;=&space;1&space;-&space;P(h_{opt}(\mathbf{x})&space;\vert&space;\mathbf{x})&space;=&space;1&space;-&space;P(y^{\ast}&space;\vert&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\epsilon_{BayesOpt}&space;=&space;1&space;-&space;P(h_{opt}(\mathbf{x})&space;\vert&space;\mathbf{x})&space;=&space;1&space;-&space;P(y^{\ast}&space;\vert&space;\mathbf{x})" title="\epsilon_{BayesOpt} = 1 - P(h_{opt}(\mathbf{x}) \vert \mathbf{x}) = 1 - P(y^{\ast} \vert \mathbf{x})" /></a>

Assume for example an email <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> can either be classified as spam <a href="https://www.codecogs.com/eqnedit.php?latex=(&plus;1)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(&plus;1)" title="(+1)" /></a> or ham <a href="https://www.codecogs.com/eqnedit.php?latex=(-1)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(-1)" title="(-1)" /></a>. For the same email <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> the conditional class probabilities are:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;&&space;P(&plus;1&space;\vert&space;\mathbf{x})&space;=&space;0.8\\&space;&&space;P(-1&space;\vert&space;\mathbf{x})&space;=&space;0.2&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;&&space;P(&plus;1&space;\vert&space;\mathbf{x})&space;=&space;0.8\\&space;&&space;P(-1&space;\vert&space;\mathbf{x})&space;=&space;0.2&space;\end{align*}" title="\begin{align*} & P(+1 \vert \mathbf{x}) = 0.8\\ & P(-1 \vert \mathbf{x}) = 0.2 \end{align*}" /></a>

In this case the Bayes optimal classifier would predict the label <a href="https://www.codecogs.com/eqnedit.php?latex=y^{\ast}=&plus;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y^{\ast}=&plus;1" title="y^{\ast}=+1" /></a> as it is most likely, and its error rate would be <a href="https://www.codecogs.com/eqnedit.php?latex=\epsilon_{BayesOpt}&space;=&space;0.2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\epsilon_{BayesOpt}&space;=&space;0.2" title="\epsilon_{BayesOpt} = 0.2" /></a>.

Why is the Bayes optimal classifier interesting, if it cannot be used in practice? The reason is that it provides a highly informative lower bound of the error rate. With the same feature representation no classifier can obtain a lower error. We will use this fact to analyze the error rate of the knn classifier.





























































