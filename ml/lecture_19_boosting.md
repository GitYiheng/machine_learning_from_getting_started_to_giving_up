# Boosting

## Boosting Reduces Bias

**Scenario**: Hypothesis class <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{H}" title="\mathbb{H}" /></a>, whose set of classifiers has large bias and the training error is high (e.g. CART trees with very limited depth.)

**Famous question**: In his machine learning class project in 1988 Michael Kearns famously asked the question: Can weak learners (<a href="https://www.codecogs.com/eqnedit.php?latex=H" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H" title="H" /></a>) be combined to generate a strong learner with los bias?

**Famous answer: Yes!** (Robert Schapire in 1990)

**Solution**: Create ensemble classifier <a href="https://www.codecogs.com/eqnedit.php?latex=H_{T}&space;(\overrightarrow{x})&space;=&space;\sum_{t=1}^{T}&space;\alpha_t&space;h_t&space;(\overrightarrow{x})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H_{T}&space;(\overrightarrow{x})&space;=&space;\sum_{t=1}^{T}&space;\alpha_t&space;h_t&space;(\overrightarrow{x})" title="H_{T} (\overrightarrow{x}) = \sum_{t=1}^{T} \alpha_t h_t (\overrightarrow{x})" /></a>. This ensemble classifier is built in an iterative fashion. In iteration <a href="https://www.codecogs.com/eqnedit.php?latex=t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?t" title="t" /></a>
