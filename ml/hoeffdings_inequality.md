# Basic Probability Bounds

A basic question in probability, statistics, and machine learning is the following: given a random variable <a href="https://www.codecogs.com/eqnedit.php?latex=Z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z" title="Z" /></a> with expectation <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{E}[Z]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{E}[Z]" title="\mathbb{E}[Z]" /></a>, how likely is <a href="https://www.codecogs.com/eqnedit.php?latex=Z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z" title="Z" /></a> to be close to its expectation? And more precisely, how close is it likely to be? With that in mind, these notes give a few tools for computing bounds of the form

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t)" title="\mathbb{P}(Z \geq \mathbb{E}[Z] + t)" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t)" title="\mathbb{P}(Z \leq \mathbb{E}[Z] - t)" /></a>

for <a href="https://www.codecogs.com/eqnedit.php?latex=t&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?t&space;\geq&space;0" title="t \geq 0" /></a>.

Our first bound is perhaps the most basic of all probability inequalities, and it is known as Markov's inequality. Given its basic-ness, it is perhaps unsurprising that its proof is essentially only one line.

**Proposition 1** (Markov's inequality). Let <a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;\geq&space;0" title="Z \geq 0" /></a> be a non-negative random variable. Then for all <a href="https://www.codecogs.com/eqnedit.php?latex=t&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?t&space;\geq&space;0" title="t \geq 0" /></a>,

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\geq&space;t)&space;\leq&space;\frac{\mathbb{E}[Z]}{t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\geq&space;t)&space;\leq&space;\frac{\mathbb{E}[Z]}{t}" title="\mathbb{P}(Z \geq t) \leq \frac{\mathbb{E}[Z]}{t}" /></a>.

**Proof** We note that <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\geq&space;t)&space;=&space;\mathbb{E}[\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\geq&space;t)&space;=&space;\mathbb{E}[\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}]" title="\mathbb{P}(Z \geq t) = \mathbb{E}[\mathbf{1} \{ Z \geq t \}]" /></a>, and that if <a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;\geq&space;t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;\geq&space;t" title="Z \geq t" /></a>, then it must be the case that <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{Z}{t}&space;\geq&space;1&space;\geq&space;\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{Z}{t}&space;\geq&space;1&space;\geq&space;\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}" title="\frac{Z}{t} \geq 1 \geq \mathbf{1} \{ Z \geq t \}" /></a>, while if <a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;<&space;t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;<&space;t" title="Z < t" /></a>, then we still have <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{Z}{t}&space;\geq&space;0&space;=&space;\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{Z}{t}&space;\geq&space;0&space;=&space;\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}" title="\frac{Z}{t} \geq 0 = \mathbf{1} \{ Z \geq t \}" /></a>. Thus

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\geq&space;t)&space;=&space;\mathbb{E}[\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}]&space;\leq&space;\mathbb{E}[\frac{Z}{t}]&space;=&space;\frac{\mathbb{E}[Z]}{t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\geq&space;t)&space;=&space;\mathbb{E}[\mathbf{1}&space;\{&space;Z&space;\geq&space;t&space;\}]&space;\leq&space;\mathbb{E}[\frac{Z}{t}]&space;=&space;\frac{\mathbb{E}[Z]}{t}" title="\mathbb{P}(Z \geq t) = \mathbb{E}[\mathbf{1} \{ Z \geq t \}] \leq \mathbb{E}[\frac{Z}{t}] = \frac{\mathbb{E}[Z]}{t}" /></a>,

as desired.

Essentially all other bounds on the probabilities are variations on Markovs inequality. The first variation uses second moments -- the variance -- of a random variable rather than simply its mean, and is known as Chebyshev's inequality.

**Proposition 2** (Chebyshev's inequality). Let <a href="https://www.codecogs.com/eqnedit.php?latex=Z" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z" title="Z" /></a> be any random variable with <a href="https://www.codecogs.com/eqnedit.php?latex=Var(Z)&space;<&space;\infty" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Var(Z)&space;<&space;\infty" title="Var(Z) < \infty" /></a>. Then

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t&space;\enspace&space;or&space;\enspace&space;Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t)&space;\leq&space;\frac{Var(Z)}{t^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t&space;\enspace&space;or&space;\enspace&space;Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t)&space;\leq&space;\frac{Var(Z)}{t^2}" title="\mathbb{P}(Z \geq \mathbb{E}[Z] + t \enspace or \enspace Z \leq \mathbb{E}[Z] - t) \leq \frac{Var(Z)}{t^2}" /></a>

for <a href="https://www.codecogs.com/eqnedit.php?latex=t&space;\geq&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?t&space;\geq&space;0" title="t \geq 0" /></a>.

**Proof** The result is an immediate consequence of Markov's inequality. We note that if <a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t" title="Z \geq \mathbb{E}[Z] + t" /></a>, then certainly we have <a href="https://www.codecogs.com/eqnedit.php?latex=(Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2" title="(Z - \mathbb{E}[Z])^2 \geq t^2" /></a>, and similarly if <a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t" title="Z \leq \mathbb{E}[Z] - t" /></a> we have <a href="https://www.codecogs.com/eqnedit.php?latex=(Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2" title="(Z - \mathbb{E}[Z])^2 \geq t^2" /></a>. Thus

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}(Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t&space;\enspace&space;or&space;\enspace&space;Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t)&space;=&space;\mathbb{P}((Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2)&space;\\&space;\leq&space;\frac{\mathbb{E}[(Z&space;-&space;\mathbb{E}[Z])^2]}{t^2}&space;=&space;\frac{Var(Z)}{t^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}(Z&space;\geq&space;\mathbb{E}[Z]&space;&plus;&space;t&space;\enspace&space;or&space;\enspace&space;Z&space;\leq&space;\mathbb{E}[Z]&space;-&space;t)&space;=&space;\mathbb{P}((Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2)&space;\\&space;\leq&space;\frac{\mathbb{E}[(Z&space;-&space;\mathbb{E}[Z])^2]}{t^2}&space;=&space;\frac{Var(Z)}{t^2}" title="\mathbb{P}(Z \geq \mathbb{E}[Z] + t \enspace or \enspace Z \leq \mathbb{E}[Z] - t) = \mathbb{P}((Z - \mathbb{E}[Z])^2 \geq t^2) \\ \leq \frac{\mathbb{E}[(Z - \mathbb{E}[Z])^2]}{t^2} = \frac{Var(Z)}{t^2}" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{P}((Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2)&space;\leq&space;\frac{\mathbb{E}[(Z&space;-&space;\mathbb{E}[Z])^2]}{t^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{P}((Z&space;-&space;\mathbb{E}[Z])^2&space;\geq&space;t^2)&space;\leq&space;\frac{\mathbb{E}[(Z&space;-&space;\mathbb{E}[Z])^2]}{t^2}" title="\mathbb{P}((Z - \mathbb{E}[Z])^2 \geq t^2) \leq \frac{\mathbb{E}[(Z - \mathbb{E}[Z])^2]}{t^2}" /></a> is Markov's inequality.

A nice consequence of Chebyshev's inequality is that averages of random variables with finite variance converge to their mean. Let us give an example of this fact. Suppose that <a href="https://www.codecogs.com/eqnedit.php?latex=Z_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z_i" title="Z_i" /></a> are i.i.d. and satisfy <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{E}[Z_i]&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{E}[Z_i]&space;=&space;0" title="\mathbb{E}[Z_i] = 0" /></a>. Then <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{E}[Z_i]&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{E}[Z_i]&space;=&space;0" title="\mathbb{E}[Z_i] = 0" /></a>, while if we define <a href="https://www.codecogs.com/eqnedit.php?latex=\bar{Z}&space;=&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;Z_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{Z}&space;=&space;\frac{1}{n}&space;\sum_{i=1}^{n}&space;Z_i" title="\bar{Z} = \frac{1}{n} \sum_{i=1}^{n} Z_i" /></a> then










































