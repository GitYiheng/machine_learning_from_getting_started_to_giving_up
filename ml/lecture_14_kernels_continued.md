# Kernels Continued

## Well-Defined Kernels

Here are the most common kernels:

- *Linear*: <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{x}^{\top}&space;\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{x}^{\top}&space;\mathbf{z}" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = \mathbf{x}^{\top} \mathbf{z}" /></a>
- *RBF*: <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;e^{-\frac{(\mathbf{x}&space;-&space;\mathbf{z})^2}{\sigma^2}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;e^{-\frac{(\mathbf{x}&space;-&space;\mathbf{z})^2}{\sigma^2}}" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = e^{-\frac{(\mathbf{x} - \mathbf{z})^2}{\sigma^2}}" /></a>
- *Polynomial*: <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;(1&space;&plus;&space;\mathbf{x}^{\top}&space;\mathbf{z})^d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;(1&space;&plus;&space;\mathbf{x}^{\top}&space;\mathbf{z})^d" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = (1 + \mathbf{x}^{\top} \mathbf{z})^d" /></a>

Kernels built by recursively combining one or more of the following rules are called *well-defined kernels*:

1. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{x}^{\top}&space;\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{x}^{\top}&space;\mathbf{z}" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = \mathbf{x}^{\top} \mathbf{z}" /></a>
2. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;c&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;c&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = c \mathbf{k}_1 (\mathbf{x}, \mathbf{z})" /></a>
3. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;&plus;&space;\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;&plus;&space;\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = \mathbf{k}_1 (\mathbf{x}, \mathbf{z}) + \mathbf{k}_2 (\mathbf{x}, \mathbf{z})" /></a>
4. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;g\big(\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})\big)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;g\big(\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})\big)" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = g\big(\mathbf{k}_1 (\mathbf{x}, \mathbf{z})\big)" /></a>
5. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = \mathbf{k}_1 (\mathbf{x}, \mathbf{z}) \mathbf{k}_2 (\mathbf{x}, \mathbf{z})" /></a>
6. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;f(\mathbf{x})&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;f(\mathbf{z})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;f(\mathbf{x})&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;f(\mathbf{z})" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = f(\mathbf{x}) \mathbf{k}_1 (\mathbf{x}, \mathbf{z}) f(\mathbf{z})" /></a>
7. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;e^{\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;e^{\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})}" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = e^{\mathbf{k}_1 (\mathbf{x}, \mathbf{z})}" /></a>
8. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{x}^{\top}&space;\mathbf{A}&space;\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}(\mathbf{x},&space;\mathbf{z})&space;=&space;\mathbf{x}^{\top}&space;\mathbf{A}&space;\mathbf{z}" title="\mathbf{k}(\mathbf{x}, \mathbf{z}) = \mathbf{x}^{\top} \mathbf{A} \mathbf{z}" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=k_1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k_1" title="k_1" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=k_2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k_2" title="k_2" /></a> are well-defined kernels, <a href="https://www.codecogs.com/eqnedit.php?latex=c&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?c&space;\geq&space;0" title="c \geq 0" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=g" target="_blank"><img src="https://latex.codecogs.com/gif.latex?g" title="g" /></a> is a polynomial function with positive coefficients, <a href="https://www.codecogs.com/eqnedit.php?latex=f" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f" title="f" /></a> is any function and <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{A}&space;\succeq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{A}&space;\succeq&space;0" title="\mathbf{A} \succeq 0" /></a> is positive semi-definite. Kernel being well-defined is equivalent to the corresponding kernel matrix, <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{K}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{K}" title="\mathbf{K}" /></a>, being *positive semi-definite*, which is equivalent to any of the following statement:

1. All eigenvalues of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{K}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{K}" title="\mathbf{K}" /></a> are non-negative.
2. <a href="https://www.codecogs.com/eqnedit.php?latex=\exists" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\exists" title="\exists" /></a> real matrix <a href="https://www.codecogs.com/eqnedit.php?latex=P" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P" title="P" /></a> s.t. <a href="https://www.codecogs.com/eqnedit.php?latex=K&space;=&space;P^\top&space;P" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K&space;=&space;P^\top&space;P" title="K = P^\top P" /></a>.
3. <a href="https://www.codecogs.com/eqnedit.php?latex=\forall" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\forall" title="\forall" /></a> real vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}^\top&space;K&space;\mathbf{x}&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}^\top&space;K&space;\mathbf{x}&space;\geq&space;0" title="\mathbf{x}^\top K \mathbf{x} \geq 0" /></a>.

It is trivial to prove that linear kernel and polynomial kernel with integer <a href="https://www.codecogs.com/eqnedit.php?latex=d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?d" title="d" /></a> are both well-defined kernel.

**Theorem**. *The RBF kernel <a href="https://www.codecogs.com/eqnedit.php?latex=k(\mathbf{x},&space;\mathbf{z})&space;=&space;e^{\frac{-(\mathbf{x}&space;-&space;\mathbf{z})^2}{\sigma^2}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k(\mathbf{x},&space;\mathbf{z})&space;=&space;e^{\frac{-(\mathbf{x}&space;-&space;\mathbf{z})^2}{\sigma^2}}" title="k(\mathbf{x}, \mathbf{z}) = e^{\frac{-(\mathbf{x} - \mathbf{z})^2}{\sigma^2}}" /></a> is a well-defined kernel matrix*.

*Proof*.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;\mathbf{x}^{\top}&space;\mathbf{z}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;1}&space;\\&space;\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;\frac{2}{\sigma^2}&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;=&space;\frac{2}{\sigma^2}&space;\mathbf{x}^{\top}&space;\mathbf{z}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;2}&space;\\&space;\mathbf{k}_3&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;e^{\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})}&space;=&space;e^{\frac{2&space;\mathbf{x}^{\top}&space;\mathbf{z}}{\sigma^2}}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;7}&space;\\&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;\mathbf{x}^{\top}&space;\mathbf{z}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;1}&space;\\&space;\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;\frac{2}{\sigma^2}&space;\mathbf{k}_1&space;(\mathbf{x},&space;\mathbf{z})&space;=&space;\frac{2}{\sigma^2}&space;\mathbf{x}^{\top}&space;\mathbf{z}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;2}&space;\\&space;\mathbf{k}_3&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;e^{\mathbf{k}_2&space;(\mathbf{x},&space;\mathbf{z})}&space;=&space;e^{\frac{2&space;\mathbf{x}^{\top}&space;\mathbf{z}}{\sigma^2}}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;7}&space;\\&space;\end{align*}" title="\begin{align*} \mathbf{k}_1 (\mathbf{x}, \mathbf{z}) & = \mathbf{x}^{\top} \mathbf{z} && \text{well defined by rule 1} \\ \mathbf{k}_2 (\mathbf{x}, \mathbf{z}) & = \frac{2}{\sigma^2} \mathbf{k}_1 (\mathbf{x}, \mathbf{z}) = \frac{2}{\sigma^2} \mathbf{x}^{\top} \mathbf{z} && \text{well defined by rule 2} \\ \mathbf{k}_3 (\mathbf{x}, \mathbf{z}) & = e^{\mathbf{k}_2 (\mathbf{x}, \mathbf{z})} = e^{\frac{2 \mathbf{x}^{\top} \mathbf{z}}{\sigma^2}} && \text{well defined by rule 7} \\ \end{align*}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;\mathbf{k}_4&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;e^{-\frac{\mathbf{x}^{\top}&space;\mathbf{x}}{\sigma^2}}&space;\mathbf{k}_3&space;(\mathbf{x},&space;\mathbf{z})&space;e^{-\frac{\mathbf{z}^\top&space;\mathbf{z}}{\sigma^2}}&space;=&space;e^{-\frac{\mathbf{x}^{\top}&space;\mathbf{x}}{\sigma^2}}&space;e^{\frac{2\mathbf{x}^\top&space;\mathbf{z}}{\sigma^2}}&space;e^{-\frac{\mathbf{z}^\top&space;\mathbf{z}}{\sigma^2}}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;6&space;with&space;}&space;f(\mathbf{x})&space;=&space;e^{-\frac{\mathbf{x}^{\top}&space;\mathbf{x}}{\sigma^2}}&space;\\&space;&&space;=&space;e^{\frac{-\mathbf{x}^{\top}&space;\mathbf{x}&space;&plus;&space;2&space;\mathbf{x}^{\top}&space;\mathbf{z}&space;-&space;\mathbf{z}^{\top}&space;\mathbf{z}}{\sigma^2}}&space;=&space;e^{\frac{-(\mathbf{x}&space;-&space;\mathbf{z})^2}{\sigma^2}}&space;=&space;\mathbf{k}_{\text{RBF}}&space;(\mathbf{x},&space;\mathbf{z})&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;\mathbf{k}_4&space;(\mathbf{x},&space;\mathbf{z})&space;&&space;=&space;e^{-\frac{\mathbf{x}^{\top}&space;\mathbf{x}}{\sigma^2}}&space;\mathbf{k}_3&space;(\mathbf{x},&space;\mathbf{z})&space;e^{-\frac{\mathbf{z}^\top&space;\mathbf{z}}{\sigma^2}}&space;=&space;e^{-\frac{\mathbf{x}^{\top}&space;\mathbf{x}}{\sigma^2}}&space;e^{\frac{2\mathbf{x}^\top&space;\mathbf{z}}{\sigma^2}}&space;e^{-\frac{\mathbf{z}^\top&space;\mathbf{z}}{\sigma^2}}&space;&&&space;\text{well&space;defined&space;by&space;rule&space;6&space;with&space;}&space;f(\mathbf{x})&space;=&space;e^{-\frac{\mathbf{x}^{\top}&space;\mathbf{x}}{\sigma^2}}&space;\\&space;&&space;=&space;e^{\frac{-\mathbf{x}^{\top}&space;\mathbf{x}&space;&plus;&space;2&space;\mathbf{x}^{\top}&space;\mathbf{z}&space;-&space;\mathbf{z}^{\top}&space;\mathbf{z}}{\sigma^2}}&space;=&space;e^{\frac{-(\mathbf{x}&space;-&space;\mathbf{z})^2}{\sigma^2}}&space;=&space;\mathbf{k}_{\text{RBF}}&space;(\mathbf{x},&space;\mathbf{z})&space;\end{align*}" title="\begin{align*} \mathbf{k}_4 (\mathbf{x}, \mathbf{z}) & = e^{-\frac{\mathbf{x}^{\top} \mathbf{x}}{\sigma^2}} \mathbf{k}_3 (\mathbf{x}, \mathbf{z}) e^{-\frac{\mathbf{z}^\top \mathbf{z}}{\sigma^2}} = e^{-\frac{\mathbf{x}^{\top} \mathbf{x}}{\sigma^2}} e^{\frac{2\mathbf{x}^\top \mathbf{z}}{\sigma^2}} e^{-\frac{\mathbf{z}^\top \mathbf{z}}{\sigma^2}} && \text{well defined by rule 6 with } f(\mathbf{x}) = e^{-\frac{\mathbf{x}^{\top} \mathbf{x}}{\sigma^2}} \\ & = e^{\frac{-\mathbf{x}^{\top} \mathbf{x} + 2 \mathbf{x}^{\top} \mathbf{z} - \mathbf{z}^{\top} \mathbf{z}}{\sigma^2}} = e^{\frac{-(\mathbf{x} - \mathbf{z})^2}{\sigma^2}} = \mathbf{k}_{\text{RBF}} (\mathbf{x}, \mathbf{z}) \end{align*}" /></a>

You can even define kernels of sets, or strings or molecules.

**Theorem**. *The following kernel is defined on any two sets <a href="https://www.codecogs.com/eqnedit.php?latex=S_1,&space;S_2&space;\subseteq&space;\Omega" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_1,&space;S_2&space;\subseteq&space;\Omega" title="S_1, S_2 \subseteq \Omega" /></a>,

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}&space;(S_1,&space;S_2)&space;=&space;e^{\vert&space;S_1&space;\cap&space;S_2&space;\vert}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}&space;(S_1,&space;S_2)&space;=&space;e^{\vert&space;S_1&space;\cap&space;S_2&space;\vert}" title="\mathbf{k} (S_1, S_2) = e^{\vert S_1 \cap S_2 \vert}" /></a>

*Proof*. List out all possible samples <a href="https://www.codecogs.com/eqnedit.php?latex=\Omega" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Omega" title="\Omega" /></a> and arrange them into a sorted list. We define a vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_S&space;\in&space;\{0,&space;1\}^{\vert&space;\Omega&space;\vert}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_S&space;\in&space;\{0,&space;1\}^{\vert&space;\Omega&space;\vert}" title="\mathbf{x}_S \in \{0, 1\}^{\vert \Omega \vert}" /></a>, where each of its element indicates whether a corresponding sample is included in the set <a href="https://www.codecogs.com/eqnedit.php?latex=S" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S" title="S" /></a>. It is easy to prove that

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}&space;(S_1,&space;S_2)&space;=&space;e^{x_{S_1}^{\top}&space;x_{S_2}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}&space;(S_1,&space;S_2)&space;=&space;e^{x_{S_1}^{\top}&space;x_{S_2}}" title="\mathbf{k} (S_1, S_2) = e^{x_{S_1}^{\top} x_{S_2}}" /></a>,

which is a well-defined kernel by rule 1 and 7.

## Kernel Machines

(In practice) an algorithm can be kernelized in 3 steps:

1. Prove that the solution lies in the span of the training points (i.e. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}&space;=&space;\sum_{i=1}^{n}&space;\alpha_i&space;\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}&space;=&space;\sum_{i=1}^{n}&space;\alpha_i&space;\mathbf{x}_i" title="\mathbf{w} = \sum_{i=1}^{n} \alpha_i \mathbf{x}_i" /></a> for some <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha_i" title="\alpha_i" /></a>)
2. Rewrite the algorithm and the classifier so that all training or testing inputs <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> are only accessed in inner-products with other inputs, e.g. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i^\top&space;\mathbf{x}_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i^\top&space;\mathbf{x}_j" title="\mathbf{x}_i^\top \mathbf{x}_j" /></a>.
3. Define a kernel function and substitute <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}&space;(\mathbf{x}_i&space;,&space;\mathbf{x}_j)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}&space;(\mathbf{x}_i&space;,&space;\mathbf{x}_j)" title="\mathbf{k} (\mathbf{x}_i , \mathbf{x}_j)" /></a> for <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i^\top&space;\mathbf{x}_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i^\top&space;\mathbf{x}_j" title="\mathbf{x}_i^\top \mathbf{x}_j" /></a>.

### Kernelized Linear Regression

#### Recap

Vanilla Ordinary Least Squares Regression (OLS) [also referred to as linear regression] minimizes the following squared loss regression loss function,

<a href="https://www.codecogs.com/eqnedit.php?latex=\min_{\mathbf{w}}&space;\sum_{i=1}^{n}&space;(\mathbf{w}^{\top}&space;\mathbf{x}_i&space;-&space;y_i)^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\min_{\mathbf{w}}&space;\sum_{i=1}^{n}&space;(\mathbf{w}^{\top}&space;\mathbf{x}_i&space;-&space;y_i)^2" title="\min_{\mathbf{w}} \sum_{i=1}^{n} (\mathbf{w}^{\top} \mathbf{x}_i - y_i)^2" /></a>

to find the hyper-plane <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a>. The prediction at a test-point is simply <a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x})&space;=&space;\mathbf{w}^{\top}&space;\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x})&space;=&space;\mathbf{w}^{\top}&space;\mathbf{x}" title="h(\mathbf{x}) = \mathbf{w}^{\top} \mathbf{x}" /></a>.

If we let <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{X}&space;=&space;[\mathbf{x}_1&space;,&space;\ldots&space;,&space;\mathbf{x}_n]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{X}&space;=&space;[\mathbf{x}_1&space;,&space;\ldots&space;,&space;\mathbf{x}_n]" title="\mathbf{X} = [\mathbf{x}_1 , \ldots , \mathbf{x}_n]" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{y}&space;=&space;[y_1&space;,&space;\ldots&space;,&space;y_n]^\top" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{y}&space;=&space;[y_1&space;,&space;\ldots&space;,&space;y_n]^\top" title="\mathbf{y} = [y_1 , \ldots , y_n]^\top" /></a>, the solution of OLS can be written in closed form:

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}&space;=&space;(\mathbf{X}&space;\mathbf{X}^{\top})^{-1}&space;\mathbf{X}&space;\mathbf{y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}&space;=&space;(\mathbf{X}&space;\mathbf{X}^{\top})^{-1}&space;\mathbf{X}&space;\mathbf{y}" title="\mathbf{w} = (\mathbf{X} \mathbf{X}^{\top})^{-1} \mathbf{X} \mathbf{y}" /></a>

#### Kernelization

We begin by expressing the solution <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a> as a linear combination of the training inputs

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}&space;=&space;\sum_{i=1}^{n}&space;\alpha_i&space;\mathbf{x}_i&space;=&space;\mathbf{X}&space;\overrightarrow{\alpha}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}&space;=&space;\sum_{i=1}^{n}&space;\alpha_i&space;\mathbf{x}_i&space;=&space;\mathbf{X}&space;\overrightarrow{\alpha}" title="\mathbf{w} = \sum_{i=1}^{n} \alpha_i \mathbf{x}_i = \mathbf{X} \overrightarrow{\alpha}" /></a>

We derived that such a vector <a href="https://www.codecogs.com/eqnedit.php?latex=\overrightarrow{\alpha}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\overrightarrow{\alpha}" title="\overrightarrow{\alpha}" /></a> must always exist by observing the gradient updates that occur if <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}&space;=&space;(\mathbf{X}&space;\mathbf{X}^{\top})^{-1}&space;\mathbf{X}&space;\mathbf{y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}&space;=&space;(\mathbf{X}&space;\mathbf{X}^{\top})^{-1}&space;\mathbf{X}&space;\mathbf{y}" title="\mathbf{w} = (\mathbf{X} \mathbf{X}^{\top})^{-1} \mathbf{X} \mathbf{y}" /></a> is minimized with gradient descent and the initial vector is set to <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}_0&space;=&space;\overrightarrow{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}_0&space;=&space;\overrightarrow{0}" title="\mathbf{w}_0 = \overrightarrow{0}" /></a> (because the squared loss is convex the solution is independent of its initialization.)

Similarly, during testing a test point is only accessed through inner-products with training inputs:

<a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{z})&space;=&space;\mathbf{w}^{\top}&space;\mathbf{z}&space;=&space;\sum_{i=1}^{n}&space;\alpha_i&space;\mathbf{x}_i^\top&space;\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{z})&space;=&space;\mathbf{w}^{\top}&space;\mathbf{z}&space;=&space;\sum_{i=1}^{n}&space;\alpha_i&space;\mathbf{x}_i^\top&space;\mathbf{z}" title="h(\mathbf{z}) = \mathbf{w}^{\top} \mathbf{z} = \sum_{i=1}^{n} \alpha_i \mathbf{x}_i^\top \mathbf{z}" /></a>

We can now immediately kernelize the algorithm by substituting <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}&space;(\mathbf{x},&space;\mathbf{z})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}&space;(\mathbf{x},&space;\mathbf{z})" title="\mathbf{k} (\mathbf{x}, \mathbf{z})" /></a> for any inner-product <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}^\top&space;\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}^\top&space;\mathbf{z}" title="\mathbf{x}^\top \mathbf{z}" /></a>. It remains to show that we can also solve for the values of <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha" title="\alpha" /></a> in closed form. As it turns out, this is straight-forward.

**Theorem**. *Kernelized ordinary least squares has the solution <a href="https://www.codecogs.com/eqnedit.php?latex=\overrightarrow{\alpha}&space;=&space;\mathbf{K}^{-1}\mathbf{y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\overrightarrow{\alpha}&space;=&space;\mathbf{K}^{-1}\mathbf{y}" title="\overrightarrow{\alpha} = \mathbf{K}^{-1}\mathbf{y}" /></a>*.

*Proof*.

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;\mathbf{X}\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{w}&space;=&space;(\mathbf{X}\mathbf{X}^\top)^{-1}&space;\mathbf{X}&space;\mathbf{y}&space;&&&space;\text{multiply&space;from&space;left&space;by&space;}&space;\mathbf{X}^{\top}&space;\mathbf{X}&space;\mathbf{X}^{\top}&space;\\&space;(\mathbf{X}^\top&space;\mathbf{X})&space;(\mathbf{X}^\top&space;\mathbf{X})&space;\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{X}^{\top}&space;(\mathbf{X}&space;\mathbf{X}^{\top}&space;(\mathbf{X}&space;\mathbf{X}^{\top})^{-1})&space;\mathbf{X}&space;\mathbf{y}&space;&&&space;\text{substitute&space;}&space;\mathbf{K}&space;=&space;\mathbf{X}^{\top}&space;\mathbf{X}&space;\\&space;\mathbf{K}^2&space;\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{K}&space;\mathbf{y}&space;&&&space;\text{multiply&space;from&space;left&space;by&space;}&space;(\mathbf{K}^{-1})^2&space;\\&space;\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{K}^{-1}&space;\mathbf{y}&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;\mathbf{X}\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{w}&space;=&space;(\mathbf{X}\mathbf{X}^\top)^{-1}&space;\mathbf{X}&space;\mathbf{y}&space;&&&space;\text{multiply&space;from&space;left&space;by&space;}&space;\mathbf{X}^{\top}&space;\mathbf{X}&space;\mathbf{X}^{\top}&space;\\&space;(\mathbf{X}^\top&space;\mathbf{X})&space;(\mathbf{X}^\top&space;\mathbf{X})&space;\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{X}^{\top}&space;(\mathbf{X}&space;\mathbf{X}^{\top}&space;(\mathbf{X}&space;\mathbf{X}^{\top})^{-1})&space;\mathbf{X}&space;\mathbf{y}&space;&&&space;\text{substitute&space;}&space;\mathbf{K}&space;=&space;\mathbf{X}^{\top}&space;\mathbf{X}&space;\\&space;\mathbf{K}^2&space;\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{K}&space;\mathbf{y}&space;&&&space;\text{multiply&space;from&space;left&space;by&space;}&space;(\mathbf{K}^{-1})^2&space;\\&space;\overrightarrow{\alpha}&space;&&space;=&space;\mathbf{K}^{-1}&space;\mathbf{y}&space;\end{align*}" title="\begin{align*} \mathbf{X}\overrightarrow{\alpha} & = \mathbf{w} = (\mathbf{X}\mathbf{X}^\top)^{-1} \mathbf{X} \mathbf{y} && \text{multiply from left by } \mathbf{X}^{\top} \mathbf{X} \mathbf{X}^{\top} \\ (\mathbf{X}^\top \mathbf{X}) (\mathbf{X}^\top \mathbf{X}) \overrightarrow{\alpha} & = \mathbf{X}^{\top} (\mathbf{X} \mathbf{X}^{\top} (\mathbf{X} \mathbf{X}^{\top})^{-1}) \mathbf{X} \mathbf{y} && \text{substitute } \mathbf{K} = \mathbf{X}^{\top} \mathbf{X} \\ \mathbf{K}^2 \overrightarrow{\alpha} & = \mathbf{K} \mathbf{y} && \text{multiply from left by } (\mathbf{K}^{-1})^2 \\ \overrightarrow{\alpha} & = \mathbf{K}^{-1} \mathbf{y} \end{align*}" /></a>

Kernel regression can be extended to the kernelized version of *ridge regression*. The solution then becomes

<a href="https://www.codecogs.com/eqnedit.php?latex=\overrightarrow{\alpha}&space;=&space;(\mathbf{K}&space;&plus;&space;\tau^2&space;\mathbf{I})^{-1}&space;\mathbf{y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\overrightarrow{\alpha}&space;=&space;(\mathbf{K}&space;&plus;&space;\tau^2&space;\mathbf{I})^{-1}&space;\mathbf{y}" title="\overrightarrow{\alpha} = (\mathbf{K} + \tau^2 \mathbf{I})^{-1} \mathbf{y}" /></a>

In practice a small value of <a href="https://www.codecogs.com/eqnedit.php?latex=\tau^2&space;>&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau^2&space;>&space;0" title="\tau^2 > 0" /></a> increases stability, especially if <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{K}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{K}" title="\mathbf{K}" /></a> is not invertible. If <a href="https://www.codecogs.com/eqnedit.php?latex=\tau&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau&space;=&space;0" title="\tau = 0" /></a> kernel ridge regression, becomes kernelized ordinary least squares. Typically *kernel ridge regression* is also referred to as *kernel regression*.

#### Testing

Remember that we defined <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}&space;=&space;\mathbf{X}&space;\overrightarrow{\alpha}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}&space;=&space;\mathbf{X}&space;\overrightarrow{\alpha}" title="\mathbf{w} = \mathbf{X} \overrightarrow{\alpha}" /></a>. The prediction of a test point <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{z}" title="\mathbf{z}" /></a> then becomes

<a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{z})&space;=&space;\mathbf{z}^{\top}&space;\mathbf{w}&space;=&space;\mathbf{z}^{\top}&space;\underbrace{\mathbf{X}&space;\overrightarrow{\alpha}}_{\mathbf{w}}&space;=&space;\underbrace{\mathbf{k}_{\ast}}_{\mathbf{z}^{\top}&space;\mathbf{X}}&space;\underbrace{(\mathbf{K}&space;&plus;&space;\tau^2&space;\mathbf{I})^{-1}&space;\mathbf{y}}_{\overrightarrow{\alpha}}&space;=&space;\mathbf{k}_{\ast}&space;\overrightarrow{\alpha}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{z})&space;=&space;\mathbf{z}^{\top}&space;\mathbf{w}&space;=&space;\mathbf{z}^{\top}&space;\underbrace{\mathbf{X}&space;\overrightarrow{\alpha}}_{\mathbf{w}}&space;=&space;\underbrace{\mathbf{k}_{\ast}}_{\mathbf{z}^{\top}&space;\mathbf{X}}&space;\underbrace{(\mathbf{K}&space;&plus;&space;\tau^2&space;\mathbf{I})^{-1}&space;\mathbf{y}}_{\overrightarrow{\alpha}}&space;=&space;\mathbf{k}_{\ast}&space;\overrightarrow{\alpha}" title="h(\mathbf{z}) = \mathbf{z}^{\top} \mathbf{w} = \mathbf{z}^{\top} \underbrace{\mathbf{X} \overrightarrow{\alpha}}_{\mathbf{w}} = \underbrace{\mathbf{k}_{\ast}}_{\mathbf{z}^{\top} \mathbf{X}} \underbrace{(\mathbf{K} + \tau^2 \mathbf{I})^{-1} \mathbf{y}}_{\overrightarrow{\alpha}} = \mathbf{k}_{\ast} \overrightarrow{\alpha}" /></a>

or, if everything is in closed form:

<a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{z})&space;=&space;\mathbf{k}_{\ast}&space;(\mathbf{K}&space;&plus;&space;\tau^2&space;\mathbf{I})^{-1}&space;\mathbf{y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{z})&space;=&space;\mathbf{k}_{\ast}&space;(\mathbf{K}&space;&plus;&space;\tau^2&space;\mathbf{I})^{-1}&space;\mathbf{y}" title="h(\mathbf{z}) = \mathbf{k}_{\ast} (\mathbf{K} + \tau^2 \mathbf{I})^{-1} \mathbf{y}" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{k}_{\ast}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{k}_{\ast}" title="\mathbf{k}_{\ast}" /></a> is the kernel (vector) of the test point with the training points, i.e. the <a href="https://www.codecogs.com/eqnedit.php?latex=i^{th}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i^{th}" title="i^{th}" /></a> dimension corresponds to <a href="https://www.codecogs.com/eqnedit.php?latex=[\mathbf{k}_{\ast}]_i&space;=&space;\phi&space;(\mathbf{z})^{\top}&space;\phi&space;(\mathbf{x}_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?[\mathbf{k}_{\ast}]_i&space;=&space;\phi&space;(\mathbf{z})^{\top}&space;\phi&space;(\mathbf{x}_i)" title="[\mathbf{k}_{\ast}]_i = \phi (\mathbf{z})^{\top} \phi (\mathbf{x}_i)" /></a>, the inner-product between the test point <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{z}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{z}" title="\mathbf{z}" /></a> with the training point <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> after the mapping into feature space through <a href="https://www.codecogs.com/eqnedit.php?latex=\phi" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\phi" title="\phi" /></a>.

### Nearest Neighbors

Quiz: Let <a href="https://www.codecogs.com/eqnedit.php?latex=D&space;=&space;\{&space;(\mathbf{x}_1,&space;y_1),&space;\ldots&space;,&space;(\mathbf{x}_n,&space;y_n)&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D&space;=&space;\{&space;(\mathbf{x}_1,&space;y_1),&space;\ldots&space;,&space;(\mathbf{x}_n,&space;y_n)&space;\}" title="D = \{ (\mathbf{x}_1, y_1), \ldots , (\mathbf{x}_n, y_n) \}" /></a>. How can you kernelize nearest neighbors (with Euclidean distances)?

## Kernel SVM

The original, **primal** SVM is a quadratic programming problem:













































































