# Kernels

Linear classifiers are great, but what if there exists no linear decision boundary? As it turns out, there is an elegant way to incorporate non-linearities into most linear classifiers.

## Handcrafted Feature Expansion

We can make linear classifiers non-linear by applying basis function (feature transformations) on the input feature vectors. Formally, for a data vector <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}&space;\in&space;\mathbb{R}^d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}&space;\in&space;\mathbb{R}^d" title="\mathbf{x} \in \mathbb{R}^d" /></a>, we apply the transformation <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}&space;\rightarrow&space;\phi&space;(\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}&space;\rightarrow&space;\phi&space;(\mathbf{x})" title="\mathbf{x} \rightarrow \phi (\mathbf{x})" /></a> where 
