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

























