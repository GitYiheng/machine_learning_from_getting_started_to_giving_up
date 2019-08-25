# The Perceptron

## Assumption

1. Binary classification (i.e. <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;\in&space;\{&space;-1,&space;&plus;1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;\in&space;\{&space;-1,&space;&plus;1&space;\}" title="y_i \in \{ -1, +1 \}" /></a>)
2. Data is linearly separable

## Classifier

<a href="https://www.codecogs.com/eqnedit.php?latex=h(x_i)&space;=&space;sign(\mathbf{w}^\top&space;\mathbf{x}_i&space;&plus;&space;b)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(x_i)&space;=&space;sign(\mathbf{w}^\top&space;\mathbf{x}_i&space;&plus;&space;b)" title="h(x_i) = sign(\mathbf{w}^\top \mathbf{x}_i + b)" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?b" title="b" /></a> is the bias term (without the bias term, the hyperplane that <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a> defines would always have to go through the origin). Dealing with <a href="https://www.codecogs.com/eqnedit.php?latex=b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?b" title="b" /></a> can be a pain, so we 'absorb' it into the feature vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a> by adding one additional *constant* dimension. Under this convention,

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> becomes <a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;\mathbf{x}_i&space;\\&space;1&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;\mathbf{x}_i&space;\\&space;1&space;\end{bmatrix}" title="\begin{bmatrix} \mathbf{x}_i \\ 1 \end{bmatrix}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a> becomes <a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;\mathbf{w}&space;\\&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;\mathbf{w}&space;\\&space;b&space;\end{bmatrix}" title="\begin{bmatrix} \mathbf{w} \\ b \end{bmatrix}" /></a>

We can verify that

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;\mathbf{x}_i&space;\\&space;1&space;\end{bmatrix}^\top&space;\begin{bmatrix}&space;\mathbf{w}&space;\\&space;b&space;\end{bmatrix}&space;=&space;\mathbf{w}^\top&space;\mathbf{x}_i&space;&plus;&space;b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;\mathbf{x}_i&space;\\&space;1&space;\end{bmatrix}^\top&space;\begin{bmatrix}&space;\mathbf{w}&space;\\&space;b&space;\end{bmatrix}&space;=&space;\mathbf{w}^\top&space;\mathbf{x}_i&space;&plus;&space;b" title="\begin{bmatrix} \mathbf{x}_i \\ 1 \end{bmatrix}^\top \begin{bmatrix} \mathbf{w} \\ b \end{bmatrix} = \mathbf{w}^\top \mathbf{x}_i + b" /></a>

Using this, we can simplify the above formulation of <a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x}_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x}_i)" title="h(\mathbf{x}_i)" /></a> to

<a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x}_i)&space;=&space;sign(\mathbf{w}^\top&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x}_i)&space;=&space;sign(\mathbf{w}^\top&space;\mathbf{x})" title="h(\mathbf{x}_i) = sign(\mathbf{w}^\top \mathbf{x})" /></a>

*Observation*: Note that

<a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;(\mathbf{w}^\top&space;\mathbf{x}_i)&space;>&space;0&space;\iff&space;\mathbf{x}_i&space;\enspace&space;is&space;\enspace&space;classified&space;\enspace&space;correctly" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;(\mathbf{w}^\top&space;\mathbf{x}_i)&space;>&space;0&space;\iff&space;\mathbf{x}_i&space;\enspace&space;is&space;\enspace&space;classified&space;\enspace&space;correctly" title="y_i (\mathbf{w}^\top \mathbf{x}_i) > 0 \iff \mathbf{x}_i \enspace is \enspace classified \enspace correctly" /></a>

where 'classified correctly' means that <a href="https://www.codecogs.com/eqnedit.php?latex=x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i" title="x_i" /></a> is on the correct side of the hyperplane defined by <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a>. Also, note that the left side depends on <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;\in&space;\{&space;-1,&space;&plus;1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;\in&space;\{&space;-1,&space;&plus;1&space;\}" title="y_i \in \{ -1, +1 \}" /></a> (it wouldn't work if, for example <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;\in&space;\{&space;0,&space;&plus;1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;\in&space;\{&space;0,&space;&plus;1&space;\}" title="y_i \in \{ 0, +1 \}" /></a>).





