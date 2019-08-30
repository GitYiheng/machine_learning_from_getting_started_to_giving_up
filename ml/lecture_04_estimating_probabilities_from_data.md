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







































