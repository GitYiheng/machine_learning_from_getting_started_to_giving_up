# Empirical Risk Minimization

## Recap

Remember the unconstrained SVM formulation

<a href="https://www.codecogs.com/eqnedit.php?latex=\min_{\mathbf{w}}&space;\underbrace{C&space;\sum_{i=1}^{n}&space;\max&space;[1&space;-&space;y_i&space;\underbrace{(w^\top&space;\mathbf{x}_i&space;&plus;&space;b)}_{h(\mathbf{x}_i)}&space;,&space;0]}_{\text{Hinge-Loss}}&space;&plus;&space;\underbrace{\|&space;w&space;\|_z^2}_{\ell_2-Rgularizer}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\min_{\mathbf{w}}&space;\underbrace{C&space;\sum_{i=1}^{n}&space;\max&space;[1&space;-&space;y_i&space;\underbrace{(w^\top&space;\mathbf{x}_i&space;&plus;&space;b)}_{h(\mathbf{x}_i)}&space;,&space;0]}_{\text{Hinge-Loss}}&space;&plus;&space;\underbrace{\|&space;w&space;\|_z^2}_{\ell_2-Rgularizer}" title="\min_{\mathbf{w}} \underbrace{C \sum_{i=1}^{n} \max [1 - y_i \underbrace{(w^\top \mathbf{x}_i + b)}_{h(\mathbf{x}_i)} , 0]}_{\text{Hinge-Loss}} + \underbrace{\| w \|_z^2}_{\ell_2-Rgularizer}" /></a>

The hinge loss is the SVM's error function of choice, whereas the <a href="https://www.codecogs.com/eqnedit.php?latex=\ell_2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\ell_2" title="\ell_2" /></a>-regularizer reflects the complexity of the solution, and penalizes complex solutions. This is an example of empirical risk minimization with a loss function <a href="https://www.codecogs.com/eqnedit.php?latex=\ell" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\ell" title="\ell" /></a> and a regularizer <a href="https://www.codecogs.com/eqnedit.php?latex=r" target="_blank"><img src="https://latex.codecogs.com/gif.latex?r" title="r" /></a>,

<a href="https://www.codecogs.com/eqnedit.php?latex=\min_{\mathbf{w}}&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;\underbrace{\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i),&space;y_i)}_{Loss}&space;&plus;&space;\underbrace{\lambda&space;r&space;(w)}_{Regularizer}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\min_{\mathbf{w}}&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;\underbrace{\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i),&space;y_i)}_{Loss}&space;&plus;&space;\underbrace{\lambda&space;r&space;(w)}_{Regularizer}" title="\min_{\mathbf{w}} \frac{1}{n} \sum_{i=1}^{n} \underbrace{\ell (h_{\mathbf{w}} (\mathbf{x}_i), y_i)}_{Loss} + \underbrace{\lambda r (w)}_{Regularizer}" /></a>,

where the loss function is a continuous function which penalizes training error, and the regularizer is a continuous function which penalizes classifier complexity. Here, we define <a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda" title="\lambda" /></a> as <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{C}" title="\frac{1}{C}" /></a>.

## Commonly Used Binary Classification Loss Functions

Different Machine Learning algorithms use different loss functions. Here are a few examples:

| Loss <a href="https://www.codecogs.com/eqnedit.php?latex=\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i,&space;y_i))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i,&space;y_i))" title="\ell (h_{\mathbf{w}} (\mathbf{x}_i, y_i))" /></a> | Usage | Comments |
| - | - | - |
| Hinge-Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\max&space;[1&space;-&space;h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i&space;,&space;0]^p" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\max&space;[1&space;-&space;h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i&space;,&space;0]^p" title="\max [1 - h_{\mathbf{w}} (\mathbf{x}_i) y_i , 0]^p" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Standard SVM <a href="https://www.codecogs.com/eqnedit.php?latex=(p=1)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(p=1)" title="(p=1)" /></a> <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> (Differentiable) Squared Hingeleess SVM <a href="https://www.codecogs.com/eqnedit.php?latex=(p=2)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(p=2)" title="(p=2)" /></a> | When used for Standard SVM, the loss function denotes the size of the margin between linear separator and its closest points in either class. Only differentiable everywhere with <a href="https://www.codecogs.com/eqnedit.php?latex=p=2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p=2" title="p=2" /></a>. |
| Log-Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\log&space;(1&space;&plus;&space;e^{-h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\log&space;(1&space;&plus;&space;e^{-h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i})" title="\log (1 + e^{-h_{\mathbf{w}} (\mathbf{x}_i) y_i})" /></a> | Logistic Regression | One of the most popular loss functions in Machine Learning, since its outputs are well-calibrated probabilities. |
| Exponential Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=e^{-h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?e^{-h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i}" title="e^{-h_{\mathbf{w}} (\mathbf{x}_i) y_i}" /></a> | AdaBoost | This function is very aggressive. The loss of a misprediction increases *exponentially* with the value of <a href="https://www.codecogs.com/eqnedit.php?latex=-h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?-h_{\mathbf{w}}&space;(\mathbf{x}_i)&space;y_i" title="-h_{\mathbf{w}} (\mathbf{x}_i) y_i" /></a>. This can lead to nice convergence results, for example in the case of AdaBoost, but it can also cause problems with noisy data. |
| Zero-One Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\delta&space;(\text{sign}(h_{\mathbf{w}}&space;(\mathbf{x}_i))&space;\neq&space;y_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\delta&space;(\text{sign}(h_{\mathbf{w}}&space;(\mathbf{x}_i))&space;\neq&space;y_i)" title="\delta (\text{sign}(h_{\mathbf{w}} (\mathbf{x}_i)) \neq y_i)" /></a> | Actual Classification Loss | Non-continuous and thus impractical to optimize. |

Table of Loss Function with Classification <a href="https://www.codecogs.com/eqnedit.php?latex=y&space;\in&space;\{&space;-1,&space;&plus;1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;\in&space;\{&space;-1,&space;&plus;1&space;\}" title="y \in \{ -1, +1 \}" /></a>

## Commonly Used Regression Loss Functions

Regression algorithms (where a prediction can lie anywhere on the real-number line) also have their own host of loss functions:

| Loss <a href="https://www.codecogs.com/eqnedit.php?latex=\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i&space;,&space;y_i))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\ell&space;(h_{\mathbf{w}}&space;(\mathbf{x}_i&space;,&space;y_i))" title="\ell (h_{\mathbf{w}} (\mathbf{x}_i , y_i))" /></a> | Comments |
| - | - |
| Squared Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=(h(\mathbf{x}_i)&space;-&space;y_i)^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(h(\mathbf{x}_i)&space;-&space;y_i)^2" title="(h(\mathbf{x}_i) - y_i)^2" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Most popular regression loss function <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Estimates *Mean* Label <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> ADVANTAGE: Differentiable everywhere <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> DISADVANTAGE: Somewhat sensitive to outliers/noise <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Aslo known as Ordinary Least Squares (OLS) |
| Absolute Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\vert&space;h(\mathbf{x}_i)&space;-&space;y_i&space;\vert" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\vert&space;h(\mathbf{x}_i)&space;-&space;y_i&space;\vert" title="\vert h(\mathbf{x}_i) - y_i \vert" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Also a very popular loss function <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Estimates *Median* Label <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> ADVANTAGE: Less sensitive to noise <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> DISADVANTAGE: Not differentiable at <a href="https://www.codecogs.com/eqnedit.php?latex=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?0" title="0" /></a> |
| Huber Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{2}&space;(h(\mathbf{x}_i)&space;-&space;y_i)^2&space;\quad\text{if}\enspace&space;\vert&space;h(\mathbf{x}_i)&space;-&space;y_i&space;\vert&space;<&space;\delta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{2}&space;(h(\mathbf{x}_i)&space;-&space;y_i)^2&space;\quad\text{if}\enspace&space;\vert&space;h(\mathbf{x}_i)&space;-&space;y_i&space;\vert&space;<&space;\delta" title="\frac{1}{2} (h(\mathbf{x}_i) - y_i)^2 \quad\text{if}\enspace \vert h(\mathbf{x}_i) - y_i \vert < \delta" /></a>, <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> otherwise <a href="https://www.codecogs.com/eqnedit.php?latex=\delta&space;(\vert&space;h(\mathbf{x}_i)&space;-&space;y_i&space;\vert&space;-&space;\frac{\delta}{2})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\delta&space;(\vert&space;h(\mathbf{x}_i)&space;-&space;y_i&space;\vert&space;-&space;\frac{\delta}{2})" title="\delta (\vert h(\mathbf{x}_i) - y_i \vert - \frac{\delta}{2})" /></a> | <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Also known as Smooth Absolute Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> ADVANTAGE: "Best of Both Worlds" of *Squared* and *Absolute* Loss <br> Once-differentiable <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cdot" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cdot" title="\cdot" /></a> Takes on behavior of Squared-Loss when loss is small, and Absolute Loss when loss is large. |
| Log-Cosh Loss <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\log&space;(\cosh&space;(h(\mathbf{x}_i)&space;-&space;y_i))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\log&space;(\cosh&space;(h(\mathbf{x}_i)&space;-&space;y_i))" title="\log (\cosh (h(\mathbf{x}_i) - y_i))" /></a>, <br> <a href="https://www.codecogs.com/eqnedit.php?latex=\cosh&space;(x)&space;=&space;\frac{e^{x}&space;&plus;&space;e^{-x}}{2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cosh&space;(x)&space;=&space;\frac{e^{x}&space;&plus;&space;e^{-x}}{2}" title="\cosh (x) = \frac{e^{x} + e^{-x}}{2}" /></a> | ADVANTAGE: Similar to Huber Loss, but twice differentiable everywhere |

Table of Loss Function with Regression, i.e. <a href="https://www.codecogs.com/eqnedit.php?latex=y&space;\in&space;\mathbb{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;\in&space;\mathbb{R}" title="y \in \mathbb{R}" /></a>




























