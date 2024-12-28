## Regularization Methods
Regularization methods constrain the least-squares optimization such that the coefficients shrink towards zero, *resulting in a reduced variance*.
We have two techniques to regularize the optimization:
1. **Ridge Regularization**, which aims to control the variance of our model to avoid overfitting
2. **The Lasso** (Least Absolute Shrinksage and Selection Operator), which apart from controlling the variance, is able to find a subset of relevant input variables.

### Ridge Regression
In ridge regressionm the coefficients are obtained from the following optimization problem:
$$\hat{\beta}(\lambda)=\text{argmin}\sum_{i=1}^{N}(y_i-f_L(x_i;\beta))^2+\lambda\sum_{j=1}^{p}\beta_j^2$$ 
where $\lambda$ must be greater than 0 and is a **tuning parameter**, and $\hat{\beta}$ is the vector of learned parameters. Comments on the model:
1. Ridge regression seeks to make the RSS small
2. At the same time, we hadd a second term, called the *ridge regularization*, aiming to shrink the coefficients $\beta_j$ towards 0.
3. The tuning parameter $\lambda$ controls the relative impact of the regularization term:
	- For $\lambda=0$, we have a standard linear model with no regularization
	- For $\lambda>0$, the regularization term dominates the optimization and $\beta_j$ goes towards 0.
4. As $\lambda$ increases/decreases, the corresponding model is more rigid/flexibile. $\lambda$ is chosen via cross-validation in order to find the best amount of flexibility.
**The issue with** ridge regression is that it always includes all $p$ inputs in the model *(i.e. the standardized coefficients $\beta_j$ are never zero)*.

### The Lasso
The Lasso is an alternative form of regression that allows us to choose a subset of relevant inputs. The optimization problem is:
$$\hat{\beta}(\lambda)=\text{argmin}\sum_{i=1}^{N}(y_i-f_L(x_i;\beta))^2+\lambda\sum_{j=1}^{p}|\beta_j|$$
In contrast with ridge regression, lasso is able to force some of the coefficients to be **exactly zero** when $\lambda$ is sufficiently large.Much like ridge regression, as $\lambda$ increases/decreases, the corresponding model is more rigid/flexibile. 
**Increase in $\lambda$** = more rigid model
**Decrease in $\lambda$** = more flexibile model

If $\lambda$ grows too large, the regularized model may underfit the data, hurting the performance of the model. This is because, as $\lambda$ grows large, the regularization term dominates, and a simpler model with smaller weights is fitted.
Regularization does **not** guarantee better performance.
**Adding a new feature will always result in equal or better performance on the *training* set**.