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

Although the Bayes optimal classifier is as good as it gets





























































