# Empirical Risk Minimization

## Recap

Remember the unconstrained SVM formulation

<a href="https://www.codecogs.com/eqnedit.php?latex=\min_{\mathbf{w}}&space;\underbrace{C&space;\sum_{i=1}^{n}&space;\max&space;[1&space;-&space;y_i&space;\underbrace{(w^\top&space;\mathbf{x}_i&space;&plus;&space;b)}_{h(\mathbf{x}_i)}&space;,&space;0]}_{\text{Hinge-Loss}}&space;&plus;&space;\underbrace{\|&space;w&space;\|_z^2}_{\ell_2-Rgularizer}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\min_{\mathbf{w}}&space;\underbrace{C&space;\sum_{i=1}^{n}&space;\max&space;[1&space;-&space;y_i&space;\underbrace{(w^\top&space;\mathbf{x}_i&space;&plus;&space;b)}_{h(\mathbf{x}_i)}&space;,&space;0]}_{\text{Hinge-Loss}}&space;&plus;&space;\underbrace{\|&space;w&space;\|_z^2}_{\ell_2-Rgularizer}" title="\min_{\mathbf{w}} \underbrace{C \sum_{i=1}^{n} \max [1 - y_i \underbrace{(w^\top \mathbf{x}_i + b)}_{h(\mathbf{x}_i)} , 0]}_{\text{Hinge-Loss}} + \underbrace{\| w \|_z^2}_{\ell_2-Rgularizer}" /></a>

The hinge loss is the SVM's error function of choice, whereas the <a href="https://www.codecogs.com/eqnedit.php?latex=\ell_2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\ell_2" title="\ell_2" /></a>-regularizer reflects the complexity of the solution, and penalizes complex solutions. This is an example of empirical risk minimization with a loss function <a href="https://www.codecogs.com/eqnedit.php?latex=\ell" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\ell" title="\ell" /></a> and a regularizer <a href="https://www.codecogs.com/eqnedit.php?latex=r" target="_blank"><img src="https://latex.codecogs.com/gif.latex?r" title="r" /></a>,

<a href="https://www.codecogs.com/eqnedit.php?latex=\min_{\mathbf{w}}&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;\underbrace{\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i),&space;y_i)}_{Loss}&space;&plus;&space;\underbrace{\lambda&space;r&space;(w)}_{Regularizer}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\min_{\mathbf{w}}&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;\underbrace{\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i),&space;y_i)}_{Loss}&space;&plus;&space;\underbrace{\lambda&space;r&space;(w)}_{Regularizer}" title="\min_{\mathbf{w}} \frac{1}{n} \sum_{i=1}^{n} \underbrace{\ell (h_{\mathbf{w}} (\mathbf{x}_i), y_i)}_{Loss} + \underbrace{\lambda r (w)}_{Regularizer}" /></a>,

where the loss function is a continuous function which penalizes training error, and the regularizer is a continuous function which penalizes classifier complexity. Here, we define <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a> as <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{C}" title="\frac{1}{C}" /></a>.

## Commonly Used Binary Classification Loss Functions

Different Machine Learning algorithms use different loss functions. Here are a few examples:

| Loss | | |



































