# Gaussian Processes

## Properties of Multivariate Gaussian Distributions

We first review the definition and properties of Gaussian distribution:

A Gaussian random variable <a href="https://www.codecogs.com/eqnedit.php?latex=X&space;\sim&space;\mathcal{N}&space;(\mu&space;,&space;\Sigma)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X&space;\sim&space;\mathcal{N}&space;(\mu&space;,&space;\Sigma)" title="X \sim \mathcal{N} (\mu , \Sigma)" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=\mu" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu" title="\mu" /></a> is the mean and <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> is the covariance matrix has the following probability density function:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(x;&space;\mu&space;,&space;\Sigma)&space;=&space;\frac{1}{(2\pi)^{\frac{d}{2}}&space;\vert&space;\Sigma&space;\vert}&space;e^{-\frac{1}{2}&space;\big(&space;(x&space;-&space;\mu)^{\top}&space;\Sigma^{-1}&space;(x&space;-&space;\mu)&space;\big)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(x;&space;\mu&space;,&space;\Sigma)&space;=&space;\frac{1}{(2\pi)^{\frac{d}{2}}&space;\vert&space;\Sigma&space;\vert}&space;e^{-\frac{1}{2}&space;\big(&space;(x&space;-&space;\mu)^{\top}&space;\Sigma^{-1}&space;(x&space;-&space;\mu)&space;\big)}" title="P(x; \mu , \Sigma) = \frac{1}{(2\pi)^{\frac{d}{2}} \vert \Sigma \vert} e^{-\frac{1}{2} \big( (x - \mu)^{\top} \Sigma^{-1} (x - \mu) \big)}" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\vert&space;\Sigma&space;\vert" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\vert&space;\Sigma&space;\vert" title="\vert \Sigma \vert" /></a> is the determinant of <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a>.

The Gaussian distribution occurs very often in real world data. This is for a good reason: **the Central Limit Theorem (CLT)**. The CLT states that the arithmetic mean of <a href="https://www.codecogs.com/eqnedit.php?latex=m&space;>&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m&space;>&space;0" title="m > 0" /></a> samples is approximately normal distributed -- independent of the original sample distribution (provided it has finite mean and variance).

#### Once Gaussian Always Gaussian

Let Gaussian random variable <a href="https://www.codecogs.com/eqnedit.php?latex=y&space;=&space;\begin{bmatrix}&space;y_A&space;\\&space;y_B&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;=&space;\begin{bmatrix}&space;y_A&space;\\&space;y_B&space;\end{bmatrix}" title="y = \begin{bmatrix} y_A \\ y_B \end{bmatrix}" /></a>, mean <a href="https://www.codecogs.com/eqnedit.php?latex=\mu&space;=&space;\begin{bmatrix}&space;\mu_A&space;\\&space;\mu_B&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu&space;=&space;\begin{bmatrix}&space;\mu_A&space;\\&space;\mu_B&space;\end{bmatrix}" title="\mu = \begin{bmatrix} \mu_A \\ \mu_B \end{bmatrix}" /></a> and covariance matrix <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma&space;=&space;\begin{bmatrix}&space;\Sigma_{AA},&space;\Sigma_{AB}&space;\\&space;\Sigma_{BA},&space;\Sigma_{BB}&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma&space;=&space;\begin{bmatrix}&space;\Sigma_{AA},&space;\Sigma_{AB}&space;\\&space;\Sigma_{BA},&space;\Sigma_{BB}&space;\end{bmatrix}" title="\Sigma = \begin{bmatrix} \Sigma_{AA}, \Sigma_{AB} \\ \Sigma_{BA}, \Sigma_{BB} \end{bmatrix}" /></a>. We have the following properties:

1. **Normalization**:

<a href="https://www.codecogs.com/eqnedit.php?latex=\int_y&space;p&space;(y&space;;&space;\mu&space;,&space;\Sigma)&space;dy&space;=&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\int_y&space;p&space;(y&space;;&space;\mu&space;,&space;\Sigma)&space;dy&space;=&space;1" title="\int_y p (y ; \mu , \Sigma) dy = 1" /></a>

2. **Marginalization**: The marginal distribution <a href="https://www.codecogs.com/eqnedit.php?latex=p&space;(&space;y_A&space;)&space;=&space;\int_{y_B}&space;p&space;(y_A&space;,&space;y_B;&space;\mu&space;,&space;\Sigma)&space;d&space;y_B" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p&space;(&space;y_A&space;)&space;=&space;\int_{y_B}&space;p&space;(y_A&space;,&space;y_B;&space;\mu&space;,&space;\Sigma)&space;d&space;y_B" title="p ( y_A ) = \int_{y_B} p (y_A , y_B; \mu , \Sigma) d y_B" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=p&space;(&space;y_B&space;)&space;=&space;\int_{y_A}&space;p&space;(y_A&space;,&space;y_B;&space;\mu&space;,&space;\Sigma)&space;d&space;y_A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p&space;(&space;y_B&space;)&space;=&space;\int_{y_A}&space;p&space;(y_A&space;,&space;y_B;&space;\mu&space;,&space;\Sigma)&space;d&space;y_A" title="p ( y_B ) = \int_{y_A} p (y_A , y_B; \mu , \Sigma) d y_A" /></a> are Gaussian:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;&&space;y_A&space;\sim&space;\mathcal{N}&space;(\mu_A&space;,&space;\Sigma_{AA})&space;\\&space;&&space;y_B&space;\sim&space;\mathcal{N}&space;(\mu_B&space;,&space;\Sigma_{BB})&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;&&space;y_A&space;\sim&space;\mathcal{N}&space;(\mu_A&space;,&space;\Sigma_{AA})&space;\\&space;&&space;y_B&space;\sim&space;\mathcal{N}&space;(\mu_B&space;,&space;\Sigma_{BB})&space;\end{align*}" title="\begin{align*} & y_A \sim \mathcal{N} (\mu_A , \Sigma_{AA}) \\ & y_B \sim \mathcal{N} (\mu_B , \Sigma_{BB}) \end{align*}" /></a>

3. **Summation**: If <a href="https://www.codecogs.com/eqnedit.php?latex=y&space;\sim&space;\mathcal{N}&space;(\mu&space;,&space;\Sigma)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;\sim&space;\mathcal{N}&space;(\mu&space;,&space;\Sigma)" title="y \sim \mathcal{N} (\mu , \Sigma)" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=y'&space;\sim&space;\mathcal{N}&space;(\mu'&space;,&space;\Sigma')" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y'&space;\sim&space;\mathcal{N}&space;(\mu'&space;,&space;\Sigma')" title="y' \sim \mathcal{N} (\mu' , \Sigma')" /></a>, then

<a href="https://www.codecogs.com/eqnedit.php?latex=y&space;&plus;&space;y'&space;\sim&space;\mathcal{N}&space;(\mu&space;&plus;&space;\mu'&space;,&space;\Sigma&space;&plus;&space;\Sigma')" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;&plus;&space;y'&space;\sim&space;\mathcal{N}&space;(\mu&space;&plus;&space;\mu'&space;,&space;\Sigma&space;&plus;&space;\Sigma')" title="y + y' \sim \mathcal{N} (\mu + \mu' , \Sigma + \Sigma')" /></a>

4. **Conditioning**: The conditional distribution of <a href="https://www.codecogs.com/eqnedit.php?latex=y_A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_A" title="y_A" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=y_B" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_B" title="y_B" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=p&space;(y_A&space;\vert&space;y_B)&space;=&space;\frac{p&space;(y_A&space;,&space;y_B&space;;&space;\mu&space;,&space;\Sigma)}{&space;\int_{y_A}&space;p&space;(y_A&space;,&space;y_B&space;;&space;\mu&space;,&space;\Sigma)&space;d&space;y_A&space;}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p&space;(y_A&space;\vert&space;y_B)&space;=&space;\frac{p&space;(y_A&space;,&space;y_B&space;;&space;\mu&space;,&space;\Sigma)}{&space;\int_{y_A}&space;p&space;(y_A&space;,&space;y_B&space;;&space;\mu&space;,&space;\Sigma)&space;d&space;y_A&space;}" title="p (y_A \vert y_B) = \frac{p (y_A , y_B ; \mu , \Sigma)}{ \int_{y_A} p (y_A , y_B ; \mu , \Sigma) d y_A }" /></a>

is also Gaussian:

<a href="https://www.codecogs.com/eqnedit.php?latex=y_A&space;\vert&space;y_B&space;=&space;y_B&space;\sim&space;\mathcal{N}&space;(\mu_A&space;&plus;&space;\Sigma_{AB}&space;\Sigma_{BB}^{-1}&space;(y_B&space;-&space;\mu_B),&space;\Sigma_{AA}&space;-&space;\Sigma_{AB}&space;\Sigma_{BB}^{-1}&space;\Sigma_{BA})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_A&space;\vert&space;y_B&space;=&space;y_B&space;\sim&space;\mathcal{N}&space;(\mu_A&space;&plus;&space;\Sigma_{AB}&space;\Sigma_{BB}^{-1}&space;(y_B&space;-&space;\mu_B),&space;\Sigma_{AA}&space;-&space;\Sigma_{AB}&space;\Sigma_{BB}^{-1}&space;\Sigma_{BA})" title="y_A \vert y_B = y_B \sim \mathcal{N} (\mu_A + \Sigma_{AB} \Sigma_{BB}^{-1} (y_B - \mu_B), \Sigma_{AA} - \Sigma_{AB} \Sigma_{BB}^{-1} \Sigma_{BA})" /></a>

This property will be useful in deriving Gaussian Process predictions.

## Gaussian Process Regression

### Posterior Predictive Distribution

Consider a regression problem(s):

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;y&space;&&space;=&space;f(\mathbf{x})&space;&plus;&space;\epsilon&space;\\&space;y&space;&&space;=&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;\epsilon&space;&&&space;\text{(OLS&space;and&space;ridge&space;regression)}&space;\\&space;y&space;&&space;=&space;\mathbf{w}^{\top}&space;\phi&space;(\mathbf{x})&space;&plus;&space;\epsilon&space;&&&space;\text{(kernel&space;ridge&space;regression)}&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;y&space;&&space;=&space;f(\mathbf{x})&space;&plus;&space;\epsilon&space;\\&space;y&space;&&space;=&space;\mathbf{w}^{\top}&space;\mathbf{x}&space;&plus;&space;\epsilon&space;&&&space;\text{(OLS&space;and&space;ridge&space;regression)}&space;\\&space;y&space;&&space;=&space;\mathbf{w}^{\top}&space;\phi&space;(\mathbf{x})&space;&plus;&space;\epsilon&space;&&&space;\text{(kernel&space;ridge&space;regression)}&space;\end{align*}" title="\begin{align*} y & = f(\mathbf{x}) + \epsilon \\ y & = \mathbf{w}^{\top} \mathbf{x} + \epsilon && \text{(OLS and ridge regression)} \\ y & = \mathbf{w}^{\top} \phi (\mathbf{x}) + \epsilon && \text{(kernel ridge regression)} \end{align*}" /></a>

Recall our goal to estimate probabilities from data. So far, we have developed OLS and (kernel) ridge regression as a solution for regression problems. Those solutions give us a predictive model for **one** particular parameter <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a>.

In general, the posterior predictive distribution is

<a href="https://www.codecogs.com/eqnedit.php?latex=P(Y&space;\vert&space;D,&space;X)&space;=&space;\int_{\mathbf{w}}&space;P(Y,&space;\mathbf{w}&space;\vert&space;D,&space;X)&space;d&space;\mathbf{w}&space;=&space;\int_{\mathbf{w}}&space;P(Y&space;\vert&space;\mathbf{w},&space;D,&space;X)&space;P(\mathbf{w}&space;\vert&space;D)&space;d&space;\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(Y&space;\vert&space;D,&space;X)&space;=&space;\int_{\mathbf{w}}&space;P(Y,&space;\mathbf{w}&space;\vert&space;D,&space;X)&space;d&space;\mathbf{w}&space;=&space;\int_{\mathbf{w}}&space;P(Y&space;\vert&space;\mathbf{w},&space;D,&space;X)&space;P(\mathbf{w}&space;\vert&space;D)&space;d&space;\mathbf{w}" title="P(Y \vert D, X) = \int_{\mathbf{w}} P(Y, \mathbf{w} \vert D, X) d \mathbf{w} = \int_{\mathbf{w}} P(Y \vert \mathbf{w}, D, X) P(\mathbf{w} \vert D) d \mathbf{w}" /></a>

Unfortunately, the above is *often intractable* in closed form. However, for the special case of having a Gaussian likelihood and prior (those are the ridge regression assumptions), this expression is Gaussian and we can derive its mean and covariance. So,

<a href="https://www.codecogs.com/eqnedit.php?latex=P(y_{\ast}&space;\vert&space;D,&space;\mathbf{x})&space;\sim&space;\mathcal{N}&space;(\mu_{y_{\ast}&space;\vert&space;D}&space;,&space;\Sigma_{y_{\ast}&space;\vert&space;D})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y_{\ast}&space;\vert&space;D,&space;\mathbf{x})&space;\sim&space;\mathcal{N}&space;(\mu_{y_{\ast}&space;\vert&space;D}&space;,&space;\Sigma_{y_{\ast}&space;\vert&space;D})" title="P(y_{\ast} \vert D, \mathbf{x}) \sim \mathcal{N} (\mu_{y_{\ast} \vert D} , \Sigma_{y_{\ast} \vert D})" /></a>

where

<a href="https://www.codecogs.com/eqnedit.php?latex=\mu_{y_{\ast}&space;\vert&space;D}&space;=&space;K_{\ast}^{\top}&space;(K&space;&plus;&space;\sigma^2&space;I)^{-1}&space;y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu_{y_{\ast}&space;\vert&space;D}&space;=&space;K_{\ast}^{\top}&space;(K&space;&plus;&space;\sigma^2&space;I)^{-1}&space;y" title="\mu_{y_{\ast} \vert D} = K_{\ast}^{\top} (K + \sigma^2 I)^{-1} y" /></a>

and

<a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{y_{\ast}&space;\vert&space;D}&space;=&space;K_{\ast&space;\ast}&space;-&space;K_{\ast}^{\top}&space;(K&space;&plus;&space;\sigma^2&space;I)^{-1}&space;K_{\ast}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{y_{\ast}&space;\vert&space;D}&space;=&space;K_{\ast&space;\ast}&space;-&space;K_{\ast}^{\top}&space;(K&space;&plus;&space;\sigma^2&space;I)^{-1}&space;K_{\ast}" title="\Sigma_{y_{\ast} \vert D} = K_{\ast \ast} - K_{\ast}^{\top} (K + \sigma^2 I)^{-1} K_{\ast}" /></a>

So, instead of doing MAP (as in ridge regression) let's model the entire distribution and let's forget about <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{w}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{w}" title="\mathbf{w}" /></a> and the kernel trick by modelling <a href="https://www.codecogs.com/eqnedit.php?latex=f" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f" title="f" /></a> directly (instead of <a href="https://www.codecogs.com/eqnedit.php?latex=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y" title="y" /></a>)!

## Gaussian Process -- Definition

**Problem**: <a href="https://www.codecogs.com/eqnedit.php?latex=f" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f" title="f" /></a> is an *infinite dimensional function*! But, the multivariate Gaussian distributions is for *finite dimensional random vectors*.

**Definition**: A GP is a (potentially infinite) collection of random variables (RV) such that the joint distribution of every finite subset of RVs is multivariate Gaussian:

<a href="https://www.codecogs.com/eqnedit.php?latex=f&space;\sim&space;\text{GP}(\mu,&space;k)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f&space;\sim&space;\text{GP}(\mu,&space;k)" title="f \sim \text{GP}(\mu, k)" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\mu&space;(\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu&space;(\mathbf{x})" title="\mu (\mathbf{x})" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=k(\mathbf{x},&space;\mathbf{x}')" target="_blank"><img src="https://latex.codecogs.com/gif.latex?k(\mathbf{x},&space;\mathbf{x}')" title="k(\mathbf{x}, \mathbf{x}')" /></a> are the mean resp. covariance function! Now, in order to model the predictive distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P(f_{\ast}&space;\vert&space;\mathbf{x}_{\ast}&space;,&space;D)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(f_{\ast}&space;\vert&space;\mathbf{x}_{\ast}&space;,&space;D)" title="P(f_{\ast} \vert \mathbf{x}_{\ast} , D)" /></a> we can use a Bayesian approach by using a **GP prior**: <a href="https://www.codecogs.com/eqnedit.php?latex=P(f&space;\vert&space;\mathbf{x})&space;\sim&space;\mathcal{N}(\mu&space;,&space;\Sigma)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(f&space;\vert&space;\mathbf{x})&space;\sim&space;\mathcal{N}(\mu&space;,&space;\Sigma)" title="P(f \vert \mathbf{x}) \sim \mathcal{N}(\mu , \Sigma)" /></a> and condition it on the training data <a href="https://www.codecogs.com/eqnedit.php?latex=D" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D" title="D" /></a> to model the joint distribution of <a href="https://www.codecogs.com/eqnedit.php?latex=f&space;=&space;f&space;(X)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f&space;=&space;f&space;(X)" title="f = f (X)" /></a> (vector of training observations) and <a href="https://www.codecogs.com/eqnedit.php?latex=f_{\ast}&space;=&space;f&space;(\mathbf{x}_{\ast})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f_{\ast}&space;=&space;f&space;(\mathbf{x}_{\ast})" title="f_{\ast} = f (\mathbf{x}_{\ast})" /></a> (prediction at test input).

## Gaussian Process Regression (GPR)

We assume that, before we observe the training labels, the labels are drawn from the zero-mean prior Gaussian distribution:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;y_1&space;\\&space;y_2&space;\\&space;\vdots&space;\\&space;y_n&space;\\&space;y_t&space;\end{bmatrix}&space;\sim&space;\mathcal{N}&space;(0,&space;\Sigma)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;y_1&space;\\&space;y_2&space;\\&space;\vdots&space;\\&space;y_n&space;\\&space;y_t&space;\end{bmatrix}&space;\sim&space;\mathcal{N}&space;(0,&space;\Sigma)" title="\begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \\ y_t \end{bmatrix} \sim \mathcal{N} (0, \Sigma)" /></a>

W.I.o.g. zero-mean is always possible by subtracting the sample mean. All training and test labels are drawn from an <a href="https://www.codecogs.com/eqnedit.php?latex=(n&plus;m)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(n&plus;m)" title="(n+m)" /></a>-dimension Gaussian distribution, where <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is the number of training points, <a href="https://www.codecogs.com/eqnedit.php?latex=m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m" title="m" /></a> is the number of testing points.
Note that, the real training labels, <a href="https://www.codecogs.com/eqnedit.php?latex=y_1,\ldots,y_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_1,\ldots,y_n" title="y_1,\ldots,y_n" /></a>, we observe are samples of <a href="https://www.codecogs.com/eqnedit.php?latex=Y_1,\ldots,Y_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_1,\ldots,Y_n" title="Y_1,\ldots,Y_n" /></a>.

Whether this distribution gives us meaningful distribution or not depends on how we choose the covariance matrix <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a>. We consider the following properties of <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a>:

1. <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ij}&space;=&space;E&space;\big(&space;(Y_i&space;-&space;\mu_i)&space;(Y_j&space;-&space;\mu_j)&space;\big)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ij}&space;=&space;E&space;\big(&space;(Y_i&space;-&space;\mu_i)&space;(Y_j&space;-&space;\mu_j)&space;\big)" title="\Sigma_{ij} = E \big( (Y_i - \mu_i) (Y_j - \mu_j) \big)" /></a>.
2. <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> is always positive semi-definite.
3. <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ii}&space;=&space;\text{Var}(Y_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ii}&space;=&space;\text{Var}(Y_i)" title="\Sigma_{ii} = \text{Var}(Y_i)" /></a>, thus <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ii}&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ii}&space;\geq&space;0" title="\Sigma_{ii} \geq 0" /></a>.
4. If <a href="https://www.codecogs.com/eqnedit.php?latex=Y_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_i" title="Y_i" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=Y_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_j" title="Y_j" /></a> are very independent, i.e. <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> is very different from <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_j" title="\mathbf{x}_j" /></a>, then <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ij}&space;=&space;\Sigma_{ji}&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ij}&space;=&space;\Sigma_{ji}&space;=&space;0" title="\Sigma_{ij} = \Sigma_{ji} = 0" /></a>.
5. If <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i" title="\mathbf{x}_i" /></a> is similar to <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_j" title="\mathbf{x}_j" /></a>, then <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ij}&space;=&space;\Sigma_{ji}&space;>&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ij}&space;=&space;\Sigma_{ji}&space;>&space;0" title="\Sigma_{ij} = \Sigma_{ji} > 0" /></a>.

We can observe that this is very similar from the kernel matrix in SVMs. Therefore, we can simply let <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ij}&space;=&space;K&space;(\mathbf{x}_i&space;,&space;\mathbf{x}_j)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ij}&space;=&space;K&space;(\mathbf{x}_i&space;,&space;\mathbf{x}_j)" title="\Sigma_{ij} = K (\mathbf{x}_i , \mathbf{x}_j)" /></a>. For example, if we use RBF kernel (a.k.a. "squared exponential kernel"), then

<a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ij}&space;=&space;\tau&space;e^{\frac{-\|&space;\mathbf{x}_i&space;-&space;\mathbf{x}_j&space;\|^2}{\sigma^2}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ij}&space;=&space;\tau&space;e^{\frac{-\|&space;\mathbf{x}_i&space;-&space;\mathbf{x}_j&space;\|^2}{\sigma^2}}" title="\Sigma_{ij} = \tau e^{\frac{-\| \mathbf{x}_i - \mathbf{x}_j \|^2}{\sigma^2}}" /></a>

If we use polynomial kernel, then <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma_{ij}&space;=&space;\tau&space;(1&space;&plus;&space;\mathbf{x}_i^{\top}&space;\mathbf{x}_j)^d" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma_{ij}&space;=&space;\tau&space;(1&space;&plus;&space;\mathbf{x}_i^{\top}&space;\mathbf{x}_j)^d" title="\Sigma_{ij} = \tau (1 + \mathbf{x}_i^{\top} \mathbf{x}_j)^d" /></a>.

Thus, we can decompose <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> as <a href="https://www.codecogs.com/eqnedit.php?latex=\begin{pmatrix}&space;K&space;&&space;K_{\ast}&space;\\&space;K_{\ast}^{\top}&space;&&space;K_{\ast\ast}&space;\end{pmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{pmatrix}&space;K&space;&&space;K_{\ast}&space;\\&space;K_{\ast}^{\top}&space;&&space;K_{\ast\ast}&space;\end{pmatrix}" title="\begin{pmatrix} K & K_{\ast} \\ K_{\ast}^{\top} & K_{\ast\ast} \end{pmatrix}" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex=K" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K" title="K" /></a> is the training kernel matrix, <a href="https://www.codecogs.com/eqnedit.php?latex=K_{\ast}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K_{\ast}" title="K_{\ast}" /></a> is the training-testing kernel matrix, <a href="https://www.codecogs.com/eqnedit.php?latex=K_{\ast}^{\top}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K_{\ast}^{\top}" title="K_{\ast}^{\top}" /></a> is the testing-training kernel matrix and <a href="https://www.codecogs.com/eqnedit.php?latex=K_{\ast\ast}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K_{\ast\ast}" title="K_{\ast\ast}" /></a> is the testing kernel matrix. The conditional distribution of (noise-free) values of the latent function <a href="https://www.codecogs.com/eqnedit.php?latex=f" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f" title="f" /></a> can be written as:

<a href="https://www.codecogs.com/eqnedit.php?latex=f_{\ast}&space;\vert&space;(Y_1&space;=&space;y_1,&space;\ldots&space;,&space;Y_n&space;=&space;y_n&space;,&space;\mathbf{x}_1&space;,&space;\ldots,&space;\mathbf{x}_n&space;,&space;\mathbf{x}_t)&space;\sim&space;\mathcal{N}&space;(K_{\ast}^{\top}&space;K^{-1}&space;y&space;,&space;K_{\ast\ast}&space;-&space;K_{\ast}^{\top}&space;K^{-1}&space;K_{\ast})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f_{\ast}&space;\vert&space;(Y_1&space;=&space;y_1,&space;\ldots&space;,&space;Y_n&space;=&space;y_n&space;,&space;\mathbf{x}_1&space;,&space;\ldots,&space;\mathbf{x}_n&space;,&space;\mathbf{x}_t)&space;\sim&space;\mathcal{N}&space;(K_{\ast}^{\top}&space;K^{-1}&space;y&space;,&space;K_{\ast\ast}&space;-&space;K_{\ast}^{\top}&space;K^{-1}&space;K_{\ast})" title="f_{\ast} \vert (Y_1 = y_1, \ldots , Y_n = y_n , \mathbf{x}_1 , \ldots, \mathbf{x}_n , \mathbf{x}_t) \sim \mathcal{N} (K_{\ast}^{\top} K^{-1} y , K_{\ast\ast} - K_{\ast}^{\top} K^{-1} K_{\ast})" /></a>

where the kernel matrices <a href="https://www.codecogs.com/eqnedit.php?latex=K_{\ast}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K_{\ast}" title="K_{\ast}" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=K_{\ast\ast}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K_{\ast\ast}" title="K_{\ast\ast}" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=K" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K" title="K" /></a> are functions of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_1,\ldots,\mathbf{x}_n,\mathbf{x}_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_1,\ldots,\mathbf{x}_n,\mathbf{x}_t" title="\mathbf{x}_1,\ldots,\mathbf{x}_n,\mathbf{x}_t" /></a>.


























































