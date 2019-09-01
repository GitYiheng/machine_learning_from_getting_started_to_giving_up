# SVM

The **Support Vector Machine (SVM)** is a linear classifier that can be viewed as an extension of the **Perceptron** developed by Rosenblatt in 1958. The Perceptron guaranteed that you find **a** hyperplane if it exists. The SVM finds the **maximum margin** separating hyperplane.

*Setting*: We define a linear classifier: <a href="https://www.codecogs.com/eqnedit.php?latex=h(\mathbf{x})&space;=&space;\text{sign}(\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h(\mathbf{x})&space;=&space;\text{sign}(\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b)" title="h(\mathbf{x}) = \text{sign}(\mathbf{w}^{\top} \mathbf{x} + b)" /></a> and we assume a binary classification setting with labels <a href="https://www.codecogs.com/eqnedit.php?latex=\{&space;&plus;1,&space;-1&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\{&space;&plus;1,&space;-1&space;\}" title="\{ +1, -1 \}" /></a>.

Typically, if a data set is linearly separable, there are infinitely many separating hyperplanes. A natural question to ask is:

**Question: What is the best separating hyperplane?**

**SVM Answer: The one that maximizes the distance to the closest data points from both classes. We say it is the hyperplane with maximum margin.**

## Margin

We already saw the definition of a *margin* in the context of the *Perceptron*. A hyperplane is defined through <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?b" title="b" /></a> as a set of points such that <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}&space;=&space;\{&space;\mathbf{x}&space;\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;=&space;0&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}&space;=&space;\{&space;\mathbf{x}&space;\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;=&space;0&space;\}" title="\mathcal{H} = \{ \mathbf{x} \vert \mathbf{w}^{\top} \mathbf{x} + b = 0 \}" /></a>. Let the margin <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma" title="\gamma" /></a> be defined as the distance from the hyperplane to the closest point across both classes.

**What is the distance of a point <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> to the hyperplane <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a>?**

Consider some point <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>. Let <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{d}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{d}" title="\mathbf{d}" /></a> be the vector from <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a> to <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> of minimum length. Let <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}^P" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}^P" title="\mathbf{x}^P" /></a> be the projection of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a> onto <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a>. It follows that:

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}^P&space;=&space;\mathbf{x}&space;-&space;\mathbf{d}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}^P&space;=&space;\mathbf{x}&space;-&space;\mathbf{d}" title="\mathbf{x}^P = \mathbf{x} - \mathbf{d}" /></a>.

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{d}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{d}" title="\mathbf{d}" /></a> is parallel to <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a>, so <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{d}&space;=&space;\alpha&space;\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{d}&space;=&space;\alpha&space;\mathbf{w}" title="\mathbf{d} = \alpha \mathbf{w}" /></a> for some <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha&space;\in&space;\mathbb{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha&space;\in&space;\mathbb{R}" title="\alpha \in \mathbb{R}" /></a>.

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}^P&space;\in&space;\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}^P&space;\in&space;\mathcal{H}" title="\mathbf{x}^P \in \mathcal{H}" /></a> which implies <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}^{\top}&space;\mathbf{x}^P&space;&plus;&space;b&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}^{\top}&space;\mathbf{x}^P&space;&plus;&space;b&space;=&space;0" title="\mathbf{w}^{\top} \mathbf{x}^P + b = 0" /></a>

therefore <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}^{\top}&space;\mathbf{x}^P&space;&plus;&space;b&space;=&space;\mathbf{w}^{\top}&space;(\mathbf{x}&space;-&space;\mathbf{d})&space;&plus;&space;b&space;=&space;\mathbf{w}^{\top}&space;(\mathbf{x}&space;-&space;\alpha&space;\mathbf{w})&space;&plus;&space;b&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}^{\top}&space;\mathbf{x}^P&space;&plus;&space;b&space;=&space;\mathbf{w}^{\top}&space;(\mathbf{x}&space;-&space;\mathbf{d})&space;&plus;&space;b&space;=&space;\mathbf{w}^{\top}&space;(\mathbf{x}&space;-&space;\alpha&space;\mathbf{w})&space;&plus;&space;b&space;=&space;0" title="\mathbf{w}^{\top} \mathbf{x}^P + b = \mathbf{w}^{\top} (\mathbf{x} - \mathbf{d}) + b = \mathbf{w}^{\top} (\mathbf{x} - \alpha \mathbf{w}) + b = 0" /></a>

which implies <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha&space;=&space;\frac{\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b}{\mathbf{w}^{\top}&space;\mathbf{w}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha&space;=&space;\frac{\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b}{\mathbf{w}^{\top}&space;\mathbf{w}}" title="\alpha = \frac{\mathbf{w}^{\top} \mathbf{x} + b}{\mathbf{w}^{\top} \mathbf{w}}" /></a>

The length of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{d}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{d}" title="\mathbf{d}" /></a>:

<a href="https://www.codecogs.com/eqnedit.php?latex=\|&space;\mathbf{d}&space;\|_2&space;=&space;\sqrt{\mathbf{d}^{\top}&space;\mathbf{d}}&space;=&space;\sqrt{\alpha^2&space;\mathbf{w}^{\top}&space;\mathbf{w}}&space;=&space;\frac{\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;\vert}{\sqrt{\mathbf{w}^{\top}&space;\mathbf{w}}}&space;=&space;\frac{\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;\vert}{\|&space;\mathbf{w}&space;\|_2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\|&space;\mathbf{d}&space;\|_2&space;=&space;\sqrt{\mathbf{d}^{\top}&space;\mathbf{d}}&space;=&space;\sqrt{\alpha^2&space;\mathbf{w}^{\top}&space;\mathbf{w}}&space;=&space;\frac{\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;\vert}{\sqrt{\mathbf{w}^{\top}&space;\mathbf{w}}}&space;=&space;\frac{\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;\vert}{\|&space;\mathbf{w}&space;\|_2}" title="\| \mathbf{d} \|_2 = \sqrt{\mathbf{d}^{\top} \mathbf{d}} = \sqrt{\alpha^2 \mathbf{w}^{\top} \mathbf{w}} = \frac{\vert \mathbf{w}^{\top} \mathbf{x} + b \vert}{\sqrt{\mathbf{w}^{\top} \mathbf{w}}} = \frac{\vert \mathbf{w}^{\top} \mathbf{x} + b \vert}{\| \mathbf{w} \|_2}" /></a>

Margin of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a> with respect to <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a>: <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma&space;(\mathbf{w},&space;b)&space;=&space;\operatorname*{argmin}_{\mathbf{x}&space;\in&space;D}&space;\frac{\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;\vert}{\|&space;\mathbf{w}&space;\|_2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma&space;(\mathbf{w},&space;b)&space;=&space;\operatorname*{argmin}_{\mathbf{x}&space;\in&space;D}&space;\frac{\vert&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;b&space;\vert}{\|&space;\mathbf{w}&space;\|_2}" title="\gamma (\mathbf{w}, b) = \operatorname*{argmin}_{\mathbf{x} \in D} \frac{\vert \mathbf{w}^{\top} \mathbf{x} + b \vert}{\| \mathbf{w} \|_2}" /></a>

By definition, the margin and hyperplane are scale invariant: <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma&space;(\beta&space;\mathbf{w},&space;\beta&space;b)&space;=&space;\gamma&space;(\mathbf{w},&space;b),&space;\enspace&space;\forall&space;\beta&space;\neq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma&space;(\beta&space;\mathbf{w},&space;\beta&space;b)&space;=&space;\gamma&space;(\mathbf{w},&space;b),&space;\enspace&space;\forall&space;\beta&space;\neq&space;0" title="\gamma (\beta \mathbf{w}, \beta b) = \gamma (\mathbf{w}, b), \enspace \forall \beta \neq 0" /></a>

Note that if the hyperplane is such that <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma" title="\gamma" /></a> is maximized, it must lie right in the middle of the two classes. In other words, <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma" title="\gamma" /></a> must be the distance to the closest point within *both* classes. (If not, you could move the hyperplane towards data points of the class that is further away and increase <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma" title="\gamma" /></a>, which contradicts that <a href="https://www.codecogs.com/eqnedit.php?latex=\gamma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma" title="\gamma" /></a> is maximized.)







































