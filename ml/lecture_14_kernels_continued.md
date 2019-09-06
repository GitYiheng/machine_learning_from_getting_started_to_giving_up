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
































