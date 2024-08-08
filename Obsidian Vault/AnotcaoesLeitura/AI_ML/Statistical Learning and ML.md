page: 45 (the bayes classifier)

## Books used
An Introduction to Statistical Learning
Hands on Machine Learning

# Definition of Statistical Learning
Say there is a client interested in investigating the association between advertising and sales of a particular product.
The *Advertising* data set consists of the *sales* of that product in 200 different markets along with advertising budgets for the product in each of those markets for three different media: *TV*, *radio* and *newspaper*. While it's not possible to directly increase the sales of the product, it's possible to control the advertising expenditure in each of the three media.

In this setting, the advertising budgets are ***input variables*** while *sales* is an ***output variable***.
- ***Input variables*** are typically denoted using the symbol $X$, with a subscript to distinguish them (e.g. $X_1$ is the *TV* budget, $X_2$ the radio, and $X_3$ the newspaper budget). The inputs go by different names, such as *predictors*, *independent variables*, *features*, or just *variables*.
- The ***output variable*** is often called *response* or *dependent variable*, and is typically denoted by the symbol $Y$.

**Generalizing**:
Suppose that we observe a quantitative response *Y* and *p* different predictors, $X_1, X_2, ..., X_p$. We assume there is some relationship between $Y$ and $X = (X_1, X_2, ..., X_p)$. Which can be written as:
$$
Y = f(X) + \epsilon
$$
Where $f$ is some fixed but unknown function of $X_1,...,X_p$ and $\epsilon$ is a random *error term* which is independent of $X$ and has mean zero. $f$ represents the *systematic* information that $X$ provides about $Y$.

For example, using an *Income* data set where we observe the relationship between *Income* and *Years of education*:
![[Pasted image 20240723193243.png]]
In the left, we see a plot of *income* versus *years of education* for 30 individuals in the *Income* data set. The plot suggests that it's possible to predict *income* using *years of education*.
The function $f$ that connects the input variable to the output is in general unknown. In this case it is a simulated data set so $f$ is known and shown by the blue curve on the right. The vertical lines represent the error terms $\epsilon$. Since some of the 30 observations lie above the blue curve and some lie below it, overall, the errors have approximately mean zero.

In general, the function $f$ may involve more than one input variable. This shows a 3D plot of *income* as a function of *years of education* and *seniority*:
![[Pasted image 20240723193656.png]]

## Finally the definition:
In essence, statistical learning refers to a set of approaches for estimating $f$. 

# Prediction
In many situations, a set of inputs $X$ are readily available, but the output $Y$ cannot be easily obtained. In this setting, since the error terms averages to zero, we can *predict* $Y$ using:
$$
\hat{Y} = \hat{f}(X)
$$
where $\hat{f}$ is our estimate for $f$, and $\hat{Y}$ is the resulting prediction for $Y$.
In this setting, $\hat{f}$ is often treated as a *black box*, in the sense that one is typically not concerned with the exact form of $\hat{f}$, provided that it yields accurate predictions for $Y$.

The accuracy of $\hat{Y}$ as a prediction for $Y$ depends on two quantities: *reducible error* and *irreducible error*. 
$\hat{f}$ will not be a perfect estimate for $f$, and this inaccuracy introduces some error. This error is *reducible* because we can potentially improve the accuracy of $\hat{f}$ by using the most appropriate statistical learning technique to estimate $f$. 
But because $Y$ is also a function of $\epsilon$, which, by definition cannot be predicted using $X$, even if we had a perfect estimate for $f$, it would still have some error in it. This is *irreducible error*.

The quantity $\epsilon$ may contain unmeasured variables that are useful in predicting $Y$ and also contain unmeasurable variation. And since we cannot measure them, $f$ cannot use them for its prediction.

Considering a given estimate $\hat{f}$ and a set of predictors $X$, which yields the prediction $\hat{Y} = \hat{f}(X)$ and assuming that both $\hat{f}$ and $X$ are fixed so that the only variability comes from $\epsilon$. Then it is easy to show that:
$$
\begin{align}
E(Y-\hat{Y})^2 &= E[f(X) + \epsilon - \hat{f}(X)]^2 \\
&= [f(X) - \hat{f}(X)]^2 + \mathrm{Var}(\epsilon)
\end{align}
$$
where $E(Y-\hat{Y})^2$ represents the average, or *expected value*, of the squared difference between the predicted and actual value of $Y$ which introduces the reducible error, and $\mathrm{Var}(\epsilon)$ represents the *variance* associated with the error term $\epsilon$, which gives the irreducible error.

# Inference

When the interest is to understand te association between $Y$ and $X_1, ..., X_p$, we wish to estimate $f$ but the goal is not necessarily to make predictions for $Y$. Now $\hat{f}$ cannot be treated as a black box, because the objective is to know its exact form.
These are some of questions to answer in this case:
- *Which predictors are associated with the response?* - Usually there's a chance that only a small fraction of the available predictors are substantially associated with $Y$.

- *What is the relationship between the response and each predictor?* - Some predictors may have a positive relationship with $Y$, while others the opposite.

- *Can the relationship between $Y$ and each predictor be summarized in a linear equation? Or is it more complex?*


# Methods of estimating $f$
## Training data
First we always assume we have observed a set of $n$ different data points. These observations are called the *training data* because we use it to train, or teach, our method how to estimate $f$:
Let $x_{ij}$ represent the value of the $j$th input, or predictor, for observation $i$, where $i = 1,2,...,n$ and $j=1,2,...,p$. Let $y_i$ represent the response variable for the $i$th observation. Then our training data consists of ${(x_1, y_1), (x_2, y_2), ..., (x_n, y_n)}$ where $x_i = (x_{i1}, x_{i2}, ..., x_{ip})^T$.

The goal is to apply a statistical learning method to the training data in order to estimate the unknown function $f$, e.g., find a function $\hat{f}$ such that $Y \approx \hat{f}(X)$ for any observation $(X, Y)$. 

Most statistical learning methods for this task can be characterized as either *parametric* or *non-parametric*.

## Parametric Methods
Involve a two-step model-based approach.
1. First, we make an assumption about the functional form, or shape, of $f$. For example, making a simple assumption that $f$ is linear in $X$:
$$
f(X) = \beta_0 + \beta_1 X_1 + +\beta_2 X_2 + ...  \beta_p X_p
$$
	This is a *linear model*.

2. Then, after a model has been chosen, we need a procedure that uses the training data to *fit* or *train* the model. In the case of the *linear model*, we need to estimate the parameters $\beta_0, ..., \beta_p$. That is, find the values for $\beta$ such that:
$$
Y \approx \beta_0 + \beta_1 X_1 + \beta_2 X_2 + ... + \beta_p X_p
$$
The most common approach to fitting the model is referred to as *(ordinary) least squares*.

The potential disadvantage of a parametric approach is that the model we choose will usually not match the true unknown form of $f$. If the chosen model is too far from the true $f$, the estimate will be poor. We can try to address this problem by choosing *flexible models* that can fit many different possible functional forms for $f$. 
These more complex models require estimating a greater number of parameters, which can lead to a phenomenon known as *overfitting* the data, which essentially means that they follow the errors, or noise, too closely.

## Non-Parametric methods
Non-parametric methods do not make explicit assumptions about the functional form of $f$. They seek an estimate of $f$ that gets as close as possible to the data points.
The major advantage is that they have the potential to accurately fit a wider range of possible shapes for $f$.

But non-parametric approaches requires a very large number of observations (far more than is typically needed by parametric approach) is required in order to obtain an accurate estimate for $f$.


Tradeoff between flexibility and interpretability, using different statistical learning methods:
![[Pasted image 20240806171611.png]]
\*flexibility in the sense that the higher the flexibility the wider the range of forms for $f$ is generated.

Very flexible models can lead to such complicated estimates of $f$ that it is difficult to understand how any individual predictor is associated with the response. Using a more restrictive method (such as linear model) makes it easy to understand the relationship between the predictor and the response.

## Supervised and Unsupervised Learning
### Supervised Learning
For each observation of the predictor measurement(s) $x_i$, $i = 1,...,n$, there is an associated response measurement $y_i$, which helps us *supervise* the accuracy of the prediction of future observations using our model.

### Unsupervised Learning
In this case there is no associated response $y_i$ for a vector of measurements $x_i$. One possible analysis in this case is to understand the relationships between the variables or between the observations. One statistical learning tool for this setting is *cluster analysis*, or clustering.
The goal of cluster analysis is to ascertain, on the basis of $x_1, ..., x_n$ whether the observations fall into relatively distinct groups.

### Regression versus Classification problems
Problems with a quantitative response are often referred to as *regression* problems. While those with qualitative response are *classification* problems.
There are some exceptions, such as *logistic regression* (a classification method) that it usually used with a qualitative (two-class, or binary) response.

## Assessing model accuracy
It is a very important task to decide for any given data set which statistical learning method produces the best results.
### Measuring the Quality of the Fit
In order to evaluate the performance of a statistical learning method on a given data set, we need to measure how well its predictions actually match the observed data.

In the regression setting, the most commonly-used measure is the *mean squared error* (MSE) given by
$$
MSE = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{f}(x_i))^2
$$
since the MSE is computed using the training data that was used to fit the model, this should be more accurately referred to as the *training MSE*.

For a given data set of predictors and responses $\{(x_1, y_1), ..., (x_n, y_n)\}$, we are not really interested in whether $\hat{f(x_i)} \approx y_i$, instead we want to know whether $\hat{f(x_0)} \approx y_0$, where $(x_0, y_0)$ is a *previously unseen test observation* NOT used to train the statistical learning method. So we want to use the method that gives the lowest *test MSE*, as opposed to the lowest *training MSE*.
In some settings we may have a test data set available, and then we can simply evaluate on the test observations, and select the learning method for which the test MSE is smallest.

When a given method yields a small training MSE but a large test MSE, we are *overfitting* the data. This happens because our statistical learning procedure is working too hard to find patterns that are just caused by random chance rather than by true properties of the unknown function $f$.

![[Pasted image 20240807222809.png]]

On the right, both maximum MSE values are 1.0. As flexibility increases, MSE decreases, until flexibity is too high and both MSE start to increase again.


*Bias-Variance*
These approximations in the MSE curves are the result of two competing properties of statistical learning methods.
The expected test MSE, for a given value $x_0$, can always be decomposed into the sum of three fundamental quantities: the *variance* of $\hat{f}(x_0)$, the squared *bias* of $\hat{f}(x_0)$ and the variance of the error $\epsilon$. That is
$$
expectedTestMSE= E(y_0 - \hat{f}(x_0))^2 = \mathrm{Var}(\hat{f}(x_0)) + [\mathrm{Bias}(\hat{f}(x_0))]^2 + \mathrm{Var}(\epsilon)
$$

So in order to minimize the expected test error, we need to select a statistical learning method that simultaneously achieves *low variance* and *low bias*. 
- **Variance** refers to the amount by which $\hat{f}$ would change if we estimated it using a different training data set. Ideally, the estimate for $f$ should not vary too much between training sets. However, if a method has high variance then a small change in the data can result in large changes in $\hat{f}$. In general *more flexible statistical methods have higher variance*.
- **Bias** refers to the error that is introduced by approximating a real-life problem, which may be extremely complicated, by a much simpler model. Generally, more flexible methods result in less bias.
The relative rate of change of these two quantities determines whether the test MSE increases or decreases
![[Pasted image 20240807224457.png]]

This is referred to as ***bias-variance trade-off***. The challenge is to find a method for which both the variance and the squared bias are low.

### The Classification setting
Many of the concepts in regression, such as the bias-variance trade-off, transfer over.

But as $y_i$ is qualitative now, we consider the *error rate*.
Say we seek to estimate $f$ on the basis of training observations $(x_1, y_1), ..., (x_n, y_n)$ where $y_i$ is qualitative. The error rate is the proportion of mistakes that are made if we apply our estimate $\hat{f}$ to our training observations:
$$
\frac{1}{n} \sum_{i=1}^n I(y_i \neq \hat{y_i})
$$
$\hat{y}_i$ is the predicted class label and $I(y_i \neq \hat{y}_i)$ is an *indicator variable* (true=1, false=0).
If $I$ is 0, then the $i$th observation was classified correctly, otherwise it was misclassified. 

This is the *training error rate*. The same as before applies to *training* and *test* error rates. A good classifier, as well, is one for which the test error is smallest.

