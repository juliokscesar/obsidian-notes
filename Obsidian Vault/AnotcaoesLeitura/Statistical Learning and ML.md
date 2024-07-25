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