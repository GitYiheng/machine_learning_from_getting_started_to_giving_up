# Bayes Classifier and Naive Bayes

Our training consists of the set <a href="https://www.codecogs.com/eqnedit.php?latex=D&space;=&space;\{&space;(\mathbf{x}_1,&space;y_1),&space;\ldots,&space;(\mathbf{x}_n,&space;y_n)&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?D&space;=&space;\{&space;(\mathbf{x}_1,&space;y_1),&space;\ldots,&space;(\mathbf{x}_n,&space;y_n)&space;\}" title="D = \{ (\mathbf{x}_1, y_1), \ldots, (\mathbf{x}_n, y_n) \}" /></a> drawn from some unknown distribution <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a>. Because all pairs are sampled i.i.d., we obtain

<a href="https://www.codecogs.com/eqnedit.php?latex=P(D)&space;=&space;P((\mathbf{x}_1,&space;y_1),&space;\ldots,&space;(\mathbf{x}_n,&space;y_n))&space;=&space;\prod_{\alpha=1}^{n}&space;P(\mathbf{x}_{\alpha},&space;y_{\alpha})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(D)&space;=&space;P((\mathbf{x}_1,&space;y_1),&space;\ldots,&space;(\mathbf{x}_n,&space;y_n))&space;=&space;\prod_{\alpha=1}^{n}&space;P(\mathbf{x}_{\alpha},&space;y_{\alpha})" title="P(D) = P((\mathbf{x}_1, y_1), \ldots, (\mathbf{x}_n, y_n)) = \prod_{\alpha=1}^{n} P(\mathbf{x}_{\alpha}, y_{\alpha})" /></a>.

If we do have enough data, we could estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a> similar to the coin example, where we imagine a *gigantic* die that has one side for each possible value of <a href="https://www.codecogs.com/eqnedit.php?latex=(\mathbf{x},&space;y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\mathbf{x},&space;y)" title="(\mathbf{x}, y)" /></a>. We can estimate the probability that one specific side comes up through counting:

<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(\mathbf{x},&space;y)&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)}{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(\mathbf{x},&space;y)&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)}{n}" title="\hat{P}(\mathbf{x}, y) = \frac{\sum_{i=1}^{n} I(\mathbf{x}_i = \mathbf{x} \wedge y_i = y)}{n}" /></a>,

where <a href="https://www.codecogs.com/eqnedit.php?latex=I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)&space;=&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)&space;=&space;1" title="I(\mathbf{x}_i = \mathbf{x} \wedge y_i = y) = 1" /></a> if <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}_i&space;=&space;\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}_i&space;=&space;\mathbf{x}" title="\mathbf{x}_i = \mathbf{x}" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=y_i&space;=&space;y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y_i&space;=&space;y" title="y_i = y" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?0" title="0" /></a> otherwise.

Of course, if we are primarily interested in predicting the label <a href="https://www.codecogs.com/eqnedit.php?latex=y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y" title="y" /></a> from the feature <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>, we may estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(Y&space;\vert&space;X)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(Y&space;\vert&space;X)" title="P(Y \vert X)" /></a> directly instead of <a href="https://www.codecogs.com/eqnedit.php?latex=P(X,&space;Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(X,&space;Y)" title="P(X, Y)" /></a>. We can then use the Bayes Optimal Classifier for a specific <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(y&space;\vert&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(y&space;\vert&space;\mathbf{x})" title="\hat{P}(y \vert \mathbf{x})" /></a> to make predictions.

So how can we estimate <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(y&space;\vert&space;\mathbf{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(y&space;\vert&space;\mathbf{x})" title="\hat{P}(y \vert \mathbf{x})" /></a>? Previously we have derived that <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(y)&space;=&space;\frac{\sum_{i=1}^{n}&space;I(y_i&space;=&space;y)}{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(y)&space;=&space;\frac{\sum_{i=1}^{n}&space;I(y_i&space;=&space;y)}{n}" title="\hat{P}(y) = \frac{\sum_{i=1}^{n} I(y_i = y)}{n}" /></a>. Similarly, <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(\mathbf{x})&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x})}{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(\mathbf{x})&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x})}{n}" title="\hat{P}(\mathbf{x}) = \frac{\sum_{i=1}^{n} I(\mathbf{x}_i = \mathbf{x})}{n}" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(y,&space;\mathbf{x})&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)}{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(y,&space;\mathbf{x})&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)}{n}" title="\hat{P}(y, \mathbf{x}) = \frac{\sum_{i=1}^{n} I(\mathbf{x}_i = \mathbf{x} \wedge y_i = y)}{n}" /></a>. We can put these two together

<a href="https://www.codecogs.com/eqnedit.php?latex=\hat{P}(y&space;\vert&space;\mathbf{x})&space;=&space;\frac{\hat{P}(y,&space;\mathbf{x})}{P(\mathbf{x})}&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)}{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x})}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\hat{P}(y&space;\vert&space;\mathbf{x})&space;=&space;\frac{\hat{P}(y,&space;\mathbf{x})}{P(\mathbf{x})}&space;=&space;\frac{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x}&space;\wedge&space;y_i&space;=&space;y)}{\sum_{i=1}^{n}&space;I(\mathbf{x}_i&space;=&space;\mathbf{x})}" title="\hat{P}(y \vert \mathbf{x}) = \frac{\hat{P}(y, \mathbf{x})}{P(\mathbf{x})} = \frac{\sum_{i=1}^{n} I(\mathbf{x}_i = \mathbf{x} \wedge y_i = y)}{\sum_{i=1}^{n} I(\mathbf{x}_i = \mathbf{x})}" /></a>

*Problem*: But there is a big problem with this method. The MLE estimate is only good if there are many training vectors with the **same identical** features as <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>! In **high dimensional spaces** (or with continuous <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{x}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{x}" title="\mathbf{x}" /></a>), this never happens!

# Naive Bayes

We can approach this dilemma with a simple trick, and an additional assumption. The trick part is to estimate <a href="https://www.codecogs.com/eqnedit.php?latex=P(y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y)" title="P(y)" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=P(\mathbf{x}&space;\vert&space;y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\mathbf{x}&space;\vert&space;y)" title="P(\mathbf{x} \vert y)" /></a> instead, since, by Bayes rule,

<a href="https://www.codecogs.com/eqnedit.php?latex=P(y&space;\vert&space;\mathbf{x})&space;=&space;\frac{P(\mathbf{x}&space;\vert&space;y)&space;P(y)}{P(\mathbf{x})}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y&space;\vert&space;\mathbf{x})&space;=&space;\frac{P(\mathbf{x}&space;\vert&space;y)&space;P(y)}{P(\mathbf{x})}" title="P(y \vert \mathbf{x}) = \frac{P(\mathbf{x} \vert y) P(y)}{P(\mathbf{x})}" /></a>.

Recall from *Estimating Probabilities from Data* that estimating <a href="https://www.codecogs.com/eqnedit.php?latex=P(y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y)" title="P(y)" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=P(\mathbf{x}&space;\vert&space;y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\mathbf{x}&space;\vert&space;y)" title="P(\mathbf{x} \vert y)" /></a> is called *generative learning*.

Estimating <a href="https://www.codecogs.com/eqnedit.php?latex=P(y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y)" title="P(y)" /></a> is easy. For example, if <a href="https://www.codecogs.com/eqnedit.php?latex=Y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y" title="Y" /></a> takes on discrete binary values estimating <a href="https://www.codecogs.com/eqnedit.php?latex=P(Y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(Y)" title="P(Y)" /></a> reduces to coin tossing. We simply need to count how many times we observe each outcome (in this case each class):

<a href="https://www.codecogs.com/eqnedit.php?latex=P(y=c)&space;=&space;\frac{\sum_{i=1}^{n}&space;I(y_i&space;=&space;c)}{n}&space;=&space;\hat{\pi}_c" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y=c)&space;=&space;\frac{\sum_{i=1}^{n}&space;I(y_i&space;=&space;c)}{n}&space;=&space;\hat{\pi}_c" title="P(y=c) = \frac{\sum_{i=1}^{n} I(y_i = c)}{n} = \hat{\pi}_c" /></a>

Estimating <a href="https://www.codecogs.com/eqnedit.php?latex=P(\mathbf{x}&space;\vert&space;y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\mathbf{x}&space;\vert&space;y)" title="P(\mathbf{x} \vert y)" /></a>, however, is not easy! The additional assumption that we make is the *Naive Bayes assumption*.

*Naive Bayes Assumption*:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(\mathbf{x}&space;\vert&space;y)&space;=&space;\prod_{\alpha&space;=&space;1}^{d}&space;P(x_{\alpha}&space;\vert&space;y)\text{,&space;where&space;}&space;x_{\alpha}&space;=&space;[\mathbf{x}]_{\alpha}&space;\text{&space;is&space;the&space;value&space;for&space;feature&space;}&space;\alpha" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\mathbf{x}&space;\vert&space;y)&space;=&space;\prod_{\alpha&space;=&space;1}^{d}&space;P(x_{\alpha}&space;\vert&space;y)\text{,&space;where&space;}&space;x_{\alpha}&space;=&space;[\mathbf{x}]_{\alpha}&space;\text{&space;is&space;the&space;value&space;for&space;feature&space;}&space;\alpha" title="P(\mathbf{x} \vert y) = \prod_{\alpha = 1}^{d} P(x_{\alpha} \vert y)\text{, where } x_{\alpha} = [\mathbf{x}]_{\alpha} \text{ is the value for feature } \alpha" /></a>

i.e., feature values are **independent given the label**! This is a very **bold** assumption.

For example, a setting where the Naive Bayes classifier is often used is spam filtering. Here, the data are emails and the labels are *spam* or *not-spam*. The Naive Bayes assumption implies that the words in an email are conditionally independent, given that you know that an email is spam or not. Clearly this is not true. Neither the words of spam or not-spam emails are drawn independently at random. However, the resulting classifiers can work well in practice even if this assumption is violated.

So, for now, let's pretend the Naive Bayes assumption holds. Then the Bayes Classifier can be defined as

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{align*}&space;h(\mathbf{x})&space;&&space;=&space;\operatorname*{argmax}_{y}&space;P(y&space;\vert&space;\mathbf{x})&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;\frac{P(\mathbf{x}&space;\vert&space;y)&space;P(y)}{P(\mathbf{x})}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;P(\mathbf{x}&space;\vert&space;y)&space;P(y)&space;&&&space;\text{(}&space;P(\mathbf{x})&space;\text{&space;does&space;not&space;depend&space;on&space;}&space;y&space;\text{)}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;\prod_{\alpha&space;=&space;1}^{d}&space;P(x_{\alpha}&space;\vert&space;y)&space;P(y)&space;&&&space;\text{(by&space;the&space;naive&space;Bayes&space;assumption)}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;\sum_{\alpha&space;=&space;1}^{d}&space;\log&space;(P(x_{\alpha}&space;\vert&space;y))&space;&plus;&space;\log&space;(P(y))&space;&&&space;\text{(as&space;log&space;is&space;a&space;monotonic&space;function)}&space;\end{align*}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;h(\mathbf{x})&space;&&space;=&space;\operatorname*{argmax}_{y}&space;P(y&space;\vert&space;\mathbf{x})&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;\frac{P(\mathbf{x}&space;\vert&space;y)&space;P(y)}{P(\mathbf{x})}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;P(\mathbf{x}&space;\vert&space;y)&space;P(y)&space;&&&space;\text{(}&space;P(\mathbf{x})&space;\text{&space;does&space;not&space;depend&space;on&space;}&space;y&space;\text{)}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;\prod_{\alpha&space;=&space;1}^{d}&space;P(x_{\alpha}&space;\vert&space;y)&space;P(y)&space;&&&space;\text{(by&space;the&space;naive&space;Bayes&space;assumption)}&space;\\&space;&&space;=&space;\operatorname*{argmax}_{y}&space;\sum_{\alpha&space;=&space;1}^{d}&space;\log&space;(P(x_{\alpha}&space;\vert&space;y))&space;&plus;&space;\log&space;(P(y))&space;&&&space;\text{(as&space;log&space;is&space;a&space;monotonic&space;function)}&space;\end{align*}" title="\begin{align*} h(\mathbf{x}) & = \operatorname*{argmax}_{y} P(y \vert \mathbf{x}) \\ & = \operatorname*{argmax}_{y} \frac{P(\mathbf{x} \vert y) P(y)}{P(\mathbf{x})} \\ & = \operatorname*{argmax}_{y} P(\mathbf{x} \vert y) P(y) && \text{(} P(\mathbf{x}) \text{ does not depend on } y \text{)} \\ & = \operatorname*{argmax}_{y} \prod_{\alpha = 1}^{d} P(x_{\alpha} \vert y) P(y) && \text{(by the naive Bayes assumption)} \\ & = \operatorname*{argmax}_{y} \sum_{\alpha = 1}^{d} \log (P(x_{\alpha} \vert y)) + \log (P(y)) && \text{(as log is a monotonic function)} \end{align*}" /></a>

Estimating <a href="https://www.codecogs.com/eqnedit.php?latex=\log&space;(P(x_{\alpha}&space;\vert&space;y))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\log&space;(P(x_{\alpha}&space;\vert&space;y))" title="\log (P(x_{\alpha} \vert y))" /></a> is easy as we only need to consider one dimension. And estimating <a href="https://www.codecogs.com/eqnedit.php?latex=P(y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y)" title="P(y)" /></a> is not affected by the assumption.


















































