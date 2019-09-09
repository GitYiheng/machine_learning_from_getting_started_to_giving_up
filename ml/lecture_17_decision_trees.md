# Decision Trees

## Motivation for Decision Trees

Let us return to the *k-nearest neighbor classifier*. In low dimensions it is actually quite powerful: It can learn non-linear decision boundaries and naturally can handle multi-class problems. There are however a few catches: kNN uses a lot of storage (as we are required to store the entire training data), the more training data we have the slower it becomes during testing (as we need to compute distances to all training inputs), and finally we need a good distance metric.

Most data that is interesting has some inherent structure. In the k-NN case we make the assumption that similar inputs have similar neighbors. This would imply that data points of various classes are not randomly sprinkled across the space, but instead appear in clusters of more or less homogeneous class assignments. Although there are *efficient data structures* enable faster nearest neighbor search, it is important to remember that the ultimate goal of the classifier is simply to give an accurate prediction. Imagine a binary classification problem with positive and negative label, you would know that its neighbors will be positive even before you compute the distances to each one of these million distances. It is therefore sufficient to simply know that the test point is an area where all neighbors are positive, its exactly identity is irrelevant.

Decision trees are exploiting exactly that. Here, we do not store the training data, instead we use the training data to build a tree structure that recursively divides the space into regions with similar labels. The root node of the tree represents the entire data set. This set is then split roughly in half along one dimension by a simple threshold <a href="https://www.codecogs.com/eqnedit.php?latex=t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?t" title="t" /></a>. All points that have a feature value <a href="https://www.codecogs.com/eqnedit.php?latex=\geq&space;t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\geq&space;t" title="\geq t" /></a> fall into the right child node, all the others into the left child node. The threshold <a href="https://www.codecogs.com/eqnedit.php?latex=t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?t" title="t" /></a> and the dimension are chosen so that the resulting child nodes are purer in terms of class membership. Ideally all positive points fall into one child node and all negative points in the other. If this is the case, the tree is done. If not, the leaf nodes are again split until eventually all leaves are pure (i.e. all its data points contain the same label) or cannot be split any further (in the rare case with two identical points of different labels).

Decision trees have several nice advantages over nearest neighbor algorithms:

1. once the tree is constructed, the training data does not need to be stored. Instead, we can simply store how many points of each label ended up in each leaf -- typically these are pure so we just have to store the label of all points.
2. decision trees are very fast during test time, as test inputs simply need to traverse down the tree to a leaf -- the prediction is the majority label of the leaf.
3. decision trees require no metric because the splits are based on feature thresholds and not distances.

*New goal*: Build a tree that is:

1. Maximally compact
2. Only has pure leaves

Quiz: Is it always possible to find a consistent tree?

Yes, if and only if no two input vectors have identical features but different labels.

*Bad news! Find a* **minimum size** *tree is NP-Hard!!*

*Good News*: we can approximate it very effectively with a greedy strategy. We keep splitting the data to minimize an *impurity function* that measures label purity amongst the children.

## Impurity Functions

Data: <a href="https://www.codecogs.com/eqnedit.php?latex=S&space;=&space;\{&space;(\mathbf{x}_1&space;,&space;y_1),&space;\ldots&space;,&space;(\mathbf{x}_n&space;,&space;y_n)&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S&space;=&space;\{&space;(\mathbf{x}_1&space;,&space;y_1),&space;\ldots&space;,&space;(\mathbf{x}_n&space;,&space;y_n)&space;\}" title="S = \{ (\mathbf{x}_1 , y_1), \ldots , (\mathbf{x}_n , y_n) \}" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;\in&space;\{&space;1,&space;\ldots&space;,&space;c&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;\in&space;\{&space;1,&space;\ldots&space;,&space;c&space;\}" title="y_i \in \{ 1, \ldots , c \}" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=c" target="_blank"><img src="https://latex.codecogs.com/gif.latex?c" title="c" /></a> is the number of classes

### Gini Impurity

Let <a href="https://www.codecogs.com/eqnedit.php?latex=S_k&space;\subseteq&space;S" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_k&space;\subseteq&space;S" title="S_k \subseteq S" /></a> where <a href="https://www.codecogs.com/eqnedit.php?latex=S_k&space;=&space;\{&space;(\mathbf{x}&space;,&space;y)&space;\in&space;S&space;:&space;y=k&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_k&space;=&space;\{&space;(\mathbf{x}&space;,&space;y)&space;\in&space;S&space;:&space;y=k&space;\}" title="S_k = \{ (\mathbf{x} , y) \in S : y=k \}" /></a> (all inputs with labels <a href="https://www.codecogs.com/eqnedit.php?latex=k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k" title="k" /></a>)

<a href="https://www.codecogs.com/eqnedit.php?latex=S&space;=&space;S_1&space;\cup&space;\cdots&space;\cup&space;S_c" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S&space;=&space;S_1&space;\cup&space;\cdots&space;\cup&space;S_c" title="S = S_1 \cup \cdots \cup S_c" /></a>

*Define*:

<a href="https://www.codecogs.com/eqnedit.php?latex=p_k&space;=&space;\frac{\vert&space;S_k&space;\vert}{\vert&space;S&space;\vert}&space;\leftarrow&space;\text{fraction&space;of&space;inputs&space;in&space;}&space;S&space;\text{&space;with&space;label&space;}&space;k" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_k&space;=&space;\frac{\vert&space;S_k&space;\vert}{\vert&space;S&space;\vert}&space;\leftarrow&space;\text{fraction&space;of&space;inputs&space;in&space;}&space;S&space;\text{&space;with&space;label&space;}&space;k" title="p_k = \frac{\vert S_k \vert}{\vert S \vert} \leftarrow \text{fraction of inputs in } S \text{ with label } k" /></a>











































