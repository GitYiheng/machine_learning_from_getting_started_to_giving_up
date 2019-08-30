# Estimating Probabilities from Data

Remember the *Bayes Optimal classifier*: If we are provided with <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a> we can predict the most likely label for <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>, formally <a href="https://www.codecogs.com/eqnedit.php?latex=\operatorname*{argmax}_{y}&space;P(y&space;\vert&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\operatorname*{argmax}_{y}&space;P(y&space;\vert&space;\mathbf{x})" title="\operatorname*{argmax}_{y} P(y \vert \mathbf{x})" /></a>. It is therefore worth considering if we can estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a> directly from the training data. If this is possible (to a good approximation) we could then use the Bayes Optimal classifier in practice on our estimate of <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a>.

In fact, many supervised learning can be viewed as estimating <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a>. Generally, they fall into two categories:

- When we estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)&space;=&space;P(X&space;\vert&space;Y)&space;P(Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)&space;=&space;P(X&space;\vert&space;Y)&space;P(Y)" title="P(X, Y) = P(X \vert Y) P(Y)" /></a>, then we call it **generative learning**.
- When we only estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(Y&space;\vert&space;X)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(Y&space;\vert&space;X)" title="P(Y \vert X)" /></a> directly, then we call it **discriminative learning**.

So how can we estimated probability from samples?

## Sample Scenario: Coin Toss

Suppose you find a coin and it's ancient and very valuable. **Naturally*, you ask yourself, "What is the probability that this coin comes up heads when I toss it?" You toss it <a href="https://www.codecogs.com/eqnedit.php?latex=n&space;=&space;10" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n&space;=&space;10" title="n = 10" /></a> times and obtain the following sequence of outcomes: <a href="https://www.codecogs.com/eqnedit.php?latex=D&space;=&space;\{&space;H,&space;T,&space;T,&space;H,&space;H,&space;H,&space;T,&space;T,&space;T,&space;T&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D&space;=&space;\{&space;H,&space;T,&space;T,&space;H,&space;H,&space;H,&space;T,&space;T,&space;T,&space;T&space;\}" title="D = \{ H, T, T, H, H, H, T, T, T, T \}" /></a>. Based on these samples, how would you estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(H)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(H)" title="P(H)" /></a>?

We observed <a href="https://www.codecogs.com/eqnedit.php?latex=n_H&space;=&space;4" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n_H&space;=&space;4" title="n_H = 4" /></a> heads and <a href="https://www.codecogs.com/eqnedit.php?latex=n_T&space;=&space;6" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n_T&space;=&space;6" title="n_T = 6" /></a> tails. So, intuitively,

<a href="https://www.codecogs.com/eqnedit.php?latex=P(H)&space;\approx&space;\frac{n_H}{n_H&space;&plus;&space;n_T}&space;=&space;\frac{4}{10}&space;=&space;0.4" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(H)&space;\approx&space;\frac{n_H}{n_H&space;&plus;&space;n_T}&space;=&space;\frac{4}{10}&space;=&space;0.4" title="P(H) \approx \frac{n_H}{n_H + n_T} = \frac{4}{10} = 0.4" /></a>

Can we derive this more formally?

### Maximum Likelihood Estimation (MLE)

The estimator we just mentioned is the Maximum Likelihood Estimation (MLE). For MLE you typically proceed in two steps: First, you make an explicit modeling assumption about what type of distribution your data was sampled from. Second, you set the parameters of this distribution so that the data you observed is as likely as possible.

Let us return to the coin example. A natural assumption about a coin toss is that the distribution of the observed outcomes is a *binomial distribution*. The binomial distribution has two parameters <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> and it captures the distribution of <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> independent *Bernoulli* (i.e. binary) random events that have a positive outcome with probability <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>. In our case <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is the number of coin tosses, and <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> could be the probability of the coin coming up heads (e.g. <a href="https://www.codecogs.com/eqnedit.php?latex=P(H)&space;=&space;\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(H)&space;=&space;\theta" title="P(H) = \theta" /></a>). Formally, the binomial distribution is defined as

<a href="https://www.codecogs.com/eqnedit.php?latex=P(D&space;\vert&space;\theta)&space;=&space;\begin{pmatrix}&space;n_H&space;&plus;&space;n_T&space;\\&space;n_H&space;\end{pmatrix}&space;\theta^{n_H}&space;(1-\theta)^{n_T}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(D&space;\vert&space;\theta)&space;=&space;\begin{pmatrix}&space;n_H&space;&plus;&space;n_T&space;\\&space;n_H&space;\end{pmatrix}&space;\theta^{n_H}&space;(1-\theta)^{n_T}" title="P(D \vert \theta) = \begin{pmatrix} n_H + n_T \\ n_H \end{pmatrix} \theta^{n_H} (1-\theta)^{n_T}" /></a>,

and it computes the probability that we would observe exactly <a href="https://www.codecogs.com/eqnedit.php?latex=n_H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n_H" title="n_H" /></a> heads, <a href="https://www.codecogs.com/eqnedit.php?latex=n_T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n_T" title="n_T" /></a> tails, if a coin was tossed <a href="https://www.codecogs.com/eqnedit.php?latex=n&space;=&space;n_H&space;&plus;&space;n_T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n&space;=&space;n_H&space;&plus;&space;n_T" title="n = n_H + n_T" /></a> times and its probability of coming up heads is <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>.

**MLE Principle**: Find <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{\theta}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{\theta}" title="\hat{\theta}" /></a> to maximize the likelihood of the data, <a href="https://www.codecogs.com/eqnedit.php?latex=P(D;&space;\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(D;&space;\theta)" title="P(D; \theta)" /></a>:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;\hat{\theta}_{MLE}&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;P(D;&space;\theta)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\begin{pmatrix}&space;n_H&space;&plus;&space;n_T&space;\\&space;n_H&space;\end{pmatrix}&space;\theta^{n_H}&space;(1-\theta)^{n_T}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\log&space;\begin{pmatrix}&space;n_H&space;&plus;&space;n_T&space;\\&space;n_H&space;\end{pmatrix}&space;&plus;&space;n_H&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;n_T&space;\cdot&space;\log&space;(1&space;-&space;\theta)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;n_H&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;n_T&space;\cdot&space;\log&space;(1-\theta)&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;\hat{\theta}_{MLE}&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;P(D;&space;\theta)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\begin{pmatrix}&space;n_H&space;&plus;&space;n_T&space;\\&space;n_H&space;\end{pmatrix}&space;\theta^{n_H}&space;(1-\theta)^{n_T}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\log&space;\begin{pmatrix}&space;n_H&space;&plus;&space;n_T&space;\\&space;n_H&space;\end{pmatrix}&space;&plus;&space;n_H&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;n_T&space;\cdot&space;\log&space;(1&space;-&space;\theta)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;n_H&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;n_T&space;\cdot&space;\log&space;(1-\theta)&space;\end{align*}" title="\begin{align*} \hat{\theta}_{MLE} & = \operatorname*{argmax}_{\theta} P(D; \theta) \\ & = \operatorname*{argmax}_{\theta} \begin{pmatrix} n_H + n_T \\ n_H \end{pmatrix} \theta^{n_H} (1-\theta)^{n_T} \\ & = \operatorname*{argmax}_{\theta} \log \begin{pmatrix} n_H + n_T \\ n_H \end{pmatrix} + n_H \cdot \log (\theta) + n_T \cdot \log (1 - \theta) \\ & = \operatorname*{argmax}_{\theta} n_H \cdot \log (\theta) + n_T \cdot \log (1-\theta) \end{align*}" /></a>

We can then solve for <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> by taking the derivative and equating it with zero. This results in

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{n_H}{\theta}&space;=&space;\frac{n_T}{1-\theta}&space;\Rightarrow&space;n_H&space;-&space;n_H&space;\theta&space;=&space;n_T&space;\theta&space;\Rightarrow&space;\theta&space;=&space;\frac{n_H}{n_H&space;&plus;&space;n_T}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{n_H}{\theta}&space;=&space;\frac{n_T}{1-\theta}&space;\Rightarrow&space;n_H&space;-&space;n_H&space;\theta&space;=&space;n_T&space;\theta&space;\Rightarrow&space;\theta&space;=&space;\frac{n_H}{n_H&space;&plus;&space;n_T}" title="\frac{n_H}{\theta} = \frac{n_T}{1-\theta} \Rightarrow n_H - n_H \theta = n_T \theta \Rightarrow \theta = \frac{n_H}{n_H + n_T}" /></a>

A nice sanity check is that <a href="https://www.codecogs.com/eqnedit.php?latex=\theta&space;\in&space;[0,&space;1]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta&space;\in&space;[0,&space;1]" title="\theta \in [0, 1]" /></a>.

- MLE gives the explanation of the data you observed.
- If <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is large and your model/distribution is correct (that is <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a> includes the true model), then MLE finds the **true** parameters.
- But the MLE can overfit the data if <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is small. It works well when <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is large.
- If you do not have the correct model (and <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is small) then MLE can be terribly wrong!

For example, suppose you observe <a href="https://www.codecogs.com/eqnedit.php?latex=\{&space;H,&space;H,&space;H,&space;H,&space;H&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\{&space;H,&space;H,&space;H,&space;H,&space;H&space;\}" title="\{ H, H, H, H, H \}" /></a>. What is <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{\theta}_{MLE}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{\theta}_{MLE}" title="\hat{\theta}_{MLE}" /></a>?

## Simple Scenario: Coin Toss with Prior Knowledge

Assume you have a hunch that <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> is close to <a href="https://www.codecogs.com/eqnedit.php?latex=0.5" target="_blank"><img src="https://latex.codecogs.com/gif.latex?0.5" title="0.5" /></a>. But your sample size is small, so you don't trust your estimate.

*Simple fix*: Add <a href="https://www.codecogs.com/eqnedit.php?latex=m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m" title="m" /></a> imaginery throws that would result in <a href="https://www.codecogs.com/eqnedit.php?latex=\theta'" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta'" title="\theta'" /></a> (e.g. <a href="https://www.codecogs.com/eqnedit.php?latex=\theta&space;=&space;0.5" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta&space;=&space;0.5" title="\theta = 0.5" /></a>). Add <a href="https://www.codecogs.com/eqnedit.php?latex=m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m" title="m" /></a> Heads and <a href="https://www.codecogs.com/eqnedit.php?latex=m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m" title="m" /></a> Tails to your data.

<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{\theta}&space;=&space;\frac{n_H&space;&plus;&space;m}{n_H&space;&plus;&space;n_T&space;&plus;&space;2m}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{\theta}&space;=&space;\frac{n_H&space;&plus;&space;m}{n_H&space;&plus;&space;n_T&space;&plus;&space;2m}" title="\hat{\theta} = \frac{n_H + m}{n_H + n_T + 2m}" /></a>

For large <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a>, this is an insignificant change. For small <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a>, it incorporates your "prior belief" about what <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> should be. Can we derive this formally?

### The Bayesian Way

Model <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> as a **random variable**, drawn from a distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta)" title="P(\theta)" /></a>. *Note* that <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> is **not** a random variable associated with an event in a sample space. In frequentist statistics, this is forbidden. In Bayesian statistics, this is allowed and you can specify a prior belief <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta)" title="P(\theta)" /></a> defining what values you believe <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> is likely to take on.

Now, we can look at <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta&space;\vert&space;D)&space;=&space;\frac{P(D&space;\vert&space;\theta)&space;P(\theta)}{P(D)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta&space;\vert&space;D)&space;=&space;\frac{P(D&space;\vert&space;\theta)&space;P(\theta)}{P(D)}" title="P(\theta \vert D) = \frac{P(D \vert \theta) P(\theta)}{P(D)}" /></a> (recall Bayes Rule!), where

- <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta)" title="P(\theta)" /></a> is the **prior** distribution over the parameter(s) <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>, before we see any data.
- <a href="https://www.codecogs.com/eqnedit.php?latex=P(D&space;\vert&space;\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(D&space;\vert&space;\theta)" title="P(D \vert \theta)" /></a> is the **likelihood** of the data given the parameter(s) <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>.
- <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta&space;\vert&space;D)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta&space;\vert&space;D)" title="P(\theta \vert D)" /></a> is the **posterior** distribution over the parameter(s) <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> **after** we have observed the data.

A natural choice for the prior <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta)" title="P(\theta)" /></a> is the *Beta distribution*:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta)&space;=&space;\frac{\theta^{\alpha&space;-&space;1}(1-\theta)^{\beta-1}}{B(\alpha,&space;\beta)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta)&space;=&space;\frac{\theta^{\alpha&space;-&space;1}(1-\theta)^{\beta-1}}{B(\alpha,&space;\beta)}" title="P(\theta) = \frac{\theta^{\alpha - 1}(1-\theta)^{\beta-1}}{B(\alpha, \beta)}" /></a>

where <a href="https://www.codecogs.com/eqnedit.php?latex=B(\alpha,&space;\beta)&space;=&space;\frac{\Gamma&space;(\alpha)&space;\Gamma&space;(\beta)}{\Gamma&space;(\alpha&space;&plus;&space;\beta)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?B(\alpha,&space;\beta)&space;=&space;\frac{\Gamma&space;(\alpha)&space;\Gamma&space;(\beta)}{\Gamma&space;(\alpha&space;&plus;&space;\beta)}" title="B(\alpha, \beta) = \frac{\Gamma (\alpha) \Gamma (\beta)}{\Gamma (\alpha + \beta)}" /></a> is the normalization constant (if this looks scary don't worry about it, it is just there to make sure everything sums to <a href="https://www.codecogs.com/eqnedit.php?latex=1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?1" title="1" /></a> and to scare children at Halloween). Note that here we only need a distribution over a singly binary random variable <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>. (The multivariate generalization of the Beta distribution is the *Dirichlet distribution*.)

Why is the Beta distribution a good fit?

- It models probabilities (<a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> lives on <a href="https://www.codecogs.com/eqnedit.php?latex=[0,&space;1]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?[0,&space;1]" title="[0, 1]" /></a>)
- It is of the same distributional family as the binomial distribution (**conjugate prior**) <a href="https://www.codecogs.com/eqnedit.php?latex=\rightarrow" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\rightarrow" title="\rightarrow" /></a> the math will turn out nicely:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta&space;\vert&space;D)&space;\propto&space;P(D&space;\vert&space;\theta)&space;P(\theta)&space;\propto&space;\theta^{n_H&space;&plus;&space;\alpha&space;-1}&space;(1&space;-&space;\theta)^{n_T&space;&plus;&space;\beta&space;-1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta&space;\vert&space;D)&space;\propto&space;P(D&space;\vert&space;\theta)&space;P(\theta)&space;\propto&space;\theta^{n_H&space;&plus;&space;\alpha&space;-1}&space;(1&space;-&space;\theta)^{n_T&space;&plus;&space;\beta&space;-1}" title="P(\theta \vert D) \propto P(D \vert \theta) P(\theta) \propto \theta^{n_H + \alpha -1} (1 - \theta)^{n_T + \beta -1}" /></a>

So far, we have a distribution over <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>. How can we get an estimate for <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>?

### Maximum a Posteriori Probability Estimation (MAP)

For example, we can choose <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{\theta}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{\theta}" title="\hat{\theta}" /></a> to be the *most likely <a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a> given the data*.

**MAP Principle**: Find <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{\theta}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{\theta}" title="\hat{\theta}" /></a> that maximizes the posterior distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P(\theta&space;\vert&space;D)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\theta&space;\vert&space;D)" title="P(\theta \vert D)" /></a>:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;\hat{\theta}_{MAP}&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;P(\theta&space;\vert&space;D)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\log&space;P(D&space;\vert&space;\theta)&space;&plus;&space;\log&space;P(\theta)&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;\hat{\theta}_{MAP}&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;P(\theta&space;\vert&space;D)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\log&space;P(D&space;\vert&space;\theta)&space;&plus;&space;\log&space;P(\theta)&space;\end{align*}" title="\begin{align*} \hat{\theta}_{MAP} & = \operatorname*{argmax}_{\theta} P(\theta \vert D) \\ & = \operatorname*{argmax}_{\theta} \log P(D \vert \theta) + \log P(\theta) \end{align*}" /></a>

For out coin flipping scenario, we get:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;\hat{\theta}_{MAP}&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;P(\theta&space;\vert&space;D)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\frac{P(D&space;\vert&space;\theta)P(\theta)}{P(D)}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\log&space;(P(D&space;\vert&space;\theta))&space;&plus;&space;\log&space;(P(\theta))&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;n_H&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;n_T&space;\cdot&space;\log&space;(1-\theta)&space;&plus;&space;(\alpha&space;-&space;1)&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;(\beta&space;-&space;1)&space;\cdot&space;\log&space;(1&space;-&space;\theta)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;(n_H&space;&plus;&space;\alpha&space;-&space;1)&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;(n_T&space;&plus;&space;\beta&space;-&space;1)&space;\cdot&space;\log&space;(1&space;-&space;\theta)&space;\\&space;&&space;\Rightarrow&space;\hat{\theta}_{MAP}&space;=&space;\frac{n_H&space;&plus;&space;\alpha&space;-&space;1}{n_H&space;&plus;&space;n_T&space;&plus;&space;\beta&space;&plus;&space;\alpha&space;-&space;2}&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;\hat{\theta}_{MAP}&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;P(\theta&space;\vert&space;D)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\frac{P(D&space;\vert&space;\theta)P(\theta)}{P(D)}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;\log&space;(P(D&space;\vert&space;\theta))&space;&plus;&space;\log&space;(P(\theta))&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;n_H&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;n_T&space;\cdot&space;\log&space;(1-\theta)&space;&plus;&space;(\alpha&space;-&space;1)&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;(\beta&space;-&space;1)&space;\cdot&space;\log&space;(1&space;-&space;\theta)&space;\\&space;&&space;=&space;\operatorname*{argmax}_{\theta}&space;(n_H&space;&plus;&space;\alpha&space;-&space;1)&space;\cdot&space;\log&space;(\theta)&space;&plus;&space;(n_T&space;&plus;&space;\beta&space;-&space;1)&space;\cdot&space;\log&space;(1&space;-&space;\theta)&space;\\&space;&&space;\Rightarrow&space;\hat{\theta}_{MAP}&space;=&space;\frac{n_H&space;&plus;&space;\alpha&space;-&space;1}{n_H&space;&plus;&space;n_T&space;&plus;&space;\beta&space;&plus;&space;\alpha&space;-&space;2}&space;\end{align*}" title="\begin{align*} \hat{\theta}_{MAP} & = \operatorname*{argmax}_{\theta} P(\theta \vert D) \\ & = \operatorname*{argmax}_{\theta} \frac{P(D \vert \theta)P(\theta)}{P(D)} \\ & = \operatorname*{argmax}_{\theta} \log (P(D \vert \theta)) + \log (P(\theta)) \\ & = \operatorname*{argmax}_{\theta} n_H \cdot \log (\theta) + n_T \cdot \log (1-\theta) + (\alpha - 1) \cdot \log (\theta) + (\beta - 1) \cdot \log (1 - \theta) \\ & = \operatorname*{argmax}_{\theta} (n_H + \alpha - 1) \cdot \log (\theta) + (n_T + \beta - 1) \cdot \log (1 - \theta) \\ & \Rightarrow \hat{\theta}_{MAP} = \frac{n_H + \alpha - 1}{n_H + n_T + \beta + \alpha - 2} \end{align*}" /></a>

A few comments:

- The MAP estimate is identical to MLE with <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha&space;-&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha&space;-&space;1" title="\alpha - 1" /></a> hallucinated *heads* and <a href="https://www.codecogs.com/eqnedit.php?latex=\beta&space;-&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\beta&space;-&space;1" title="\beta - 1" /></a> hallucinated *tails*
- As <a href="https://www.codecogs.com/eqnedit.php?latex=n&space;\rightarrow&space;\infty" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n&space;\rightarrow&space;\infty" title="n \rightarrow \infty" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{\theta}_{MAP}&space;\rightarrow&space;\hat{\theta}_{MLE}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{\theta}_{MAP}&space;\rightarrow&space;\hat{\theta}_{MLE}" title="\hat{\theta}_{MAP} \rightarrow \hat{\theta}_{MLE}" /></a> as <a href="https://www.codecogs.com/eqnedit.php?latex=\alpha&space;-&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\alpha&space;-&space;1" title="\alpha - 1" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\beta&space;-&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\beta&space;-&space;1" title="\beta - 1" /></a> become irrelevant compared to very large <a href="https://www.codecogs.com/eqnedit.php?latex=n_H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n_H" title="n_H" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=n_T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n_T" title="n_T" /></a>.
- MAP is a great estimator if an accurate prior belief is available (and mathematically tractable).
- If <a href="https://www.codecogs.com/eqnedit.php?latex=n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n" title="n" /></a> is small, MAP can be very wrong if prior belief is wrong!












































