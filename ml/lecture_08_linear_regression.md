# Linear Regression

## Assumptions

**Data Assumption**: <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;\in&space;\mathbb{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;\in&space;\mathbb{R}" title="y_i \in \mathbb{R}" /></a>

**Model Assumption**: <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;=&space;\mathbf{w}^{\top}&space;\mathbf{x}_i&space;&plus;&space;\epsilon_i&space;\text{&space;where&space;}&space;\epsilon_i&space;\sim&space;N(0,&space;\sigma^2)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;=&space;\mathbf{w}^{\top}&space;\mathbf{x}_i&space;&plus;&space;\epsilon_i&space;\text{&space;where&space;}&space;\epsilon_i&space;\sim&space;N(0,&space;\sigma^2)" title="y_i = \mathbf{w}^{\top} \mathbf{x}_i + \epsilon_i \text{ where } \epsilon_i \sim N(0, \sigma^2)" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\Rightarrow&space;y_i&space;\vert&space;\mathbf{x}_i&space;\sim&space;N(\mathbf{w}^{\top}&space;\mathbf{x}_i&space;,&space;\sigma^2)&space;\Rightarrow&space;P(y_i&space;\vert&space;\mathbf{x}_i&space;,&space;\mathbf{w})&space;=&space;\frac{1}{\sqrt{2\pi&space;\sigma^2}}&space;e^{-\frac{(\mathbf{x}_i^{\top}&space;\mathbf{w}&space;-&space;y_i)^2}{2\sigma^2}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Rightarrow&space;y_i&space;\vert&space;\mathbf{x}_i&space;\sim&space;N(\mathbf{w}^{\top}&space;\mathbf{x}_i&space;,&space;\sigma^2)&space;\Rightarrow&space;P(y_i&space;\vert&space;\mathbf{x}_i&space;,&space;\mathbf{w})&space;=&space;\frac{1}{\sqrt{2\pi&space;\sigma^2}}&space;e^{-\frac{(\mathbf{x}_i^{\top}&space;\mathbf{w}&space;-&space;y_i)^2}{2\sigma^2}}" title="\Rightarrow y_i \vert \mathbf{x}_i \sim N(\mathbf{w}^{\top} \mathbf{x}_i , \sigma^2) \Rightarrow P(y_i \vert \mathbf{x}_i , \mathbf{w}) = \frac{1}{\sqrt{2\pi \sigma^2}} e^{-\frac{(\mathbf{x}_i^{\top} \mathbf{w} - y_i)^2}{2\sigma^2}}" /></a>

In words, we assume that the data is drawn from a "line" <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}^{\top}&space;\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}^{\top}&space;\mathbf{x}" title="\mathbf{w}^{\top} \mathbf{x}" /></a> through the origin (one can always add a bias / offset through an additional dimension, similar to the *Perceptron*. For each data point with features <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a>, the label <a href="https://www.codecogs.com/eqnedit.php?latex=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y" title="y" /></a> is drawn from a Gaussian with mean <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}^{\top}\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}^{\top}\mathbf{x}_i" title="\mathbf{w}^{\top}\mathbf{x}_i" /></a> and variance <a href="https://www.codecogs.com/eqnedit.php?latex=\sigma^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sigma^2" title="\sigma^2" /></a>. Our task is to estimate the slope <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a> from the data.

## Estimating with MLE























