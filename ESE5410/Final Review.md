## Model Selection
### Validation Set
Split the data into a *training* and *testing* set (50-50, 70-30, etc.)
**Drawbacks of the validation set approach**:
* The test MSEs estimate varies highly with how the dataset is split
* Only a proportion of the data points are used in training - may not be enough.
* The validation set testing error tends to overestimate the true test MSE.
### K-fold Cross-validation (KCV)
Randomly partition the available data samples into $K$ nearly identical parts.
For each of the $K$ portions of the dataset, *train* the model on everything but the $k$-th part, and compute *testing* error on the $k$-th part of the dataset.
The overall K-fold cross **validation estimate** is given by averaging each of the $K$ test errors.
**Advantages of K-fold over standard CV**:
* Provides less volatile estimate of test MSE
* Uses more observations in training
* Provides less overestimated test MSE
### Bootstrap Aggregation / Bagging
For a number of iterations, choose a random subset of the data to test on; train on the remainder of the data. The points used for training are said to be *in the bag*, and those used for testing are *out of bag*.
The *out of bag errors* is the average of the testing errors from all training/testing iterations.

## Regularization
### Ridge Regularization
Ridge Regression seeks to make the RSS *small* by including a term in the minimization problem that includes the parameter vector $\beta$. This term is:
$$\lambda\sum_{j=1}^p\beta^2_j$$
* When $\lambda=0$, we have the standard RSS minimiztion problem
* For $\lambda>1$, the regularization term dominates and the parameters $\beta_j$ go to $0$.
* A larger $\lambda$ will make the model more rigid by shrinking parameters $\beta_j$.
### Lasso Regularization
In contrast to ridge regularization, Lasso is able to force some of the coefficiants to be **exactly zero** when $\lambda$ is sufficiently large. *Hence, lasso is able to automatically select a subset of relevant input variables*.
Just like ridge regularization, as $\lambda$ increases, the model gets more rigid (decreased flexibility). On the other hand, when $\lambda$ is close to 0, you recover the original MSE optimization problem.

##  Calculating the Gini Index
1. For each leaf in the tree / each partition in the input space, calculate proportion of correctly classified points, multiplied by the quantity 1 minus the proportion of correctly classified points.
2. Sum each of these values **weighted by the number of points that are clasified in that group**.
3. Finally, normalize this weighted sum by the *total number of points in the dataset*.

## Model Selection
### Feature Selection
1. Best Subset Selection
Given $p$ inputs, find a subset of inputs most relevant to explain the output:
$M_0$ denotes the null model with no inputs, i.e. $\hat{y}=\hat{\beta}_0$
For $k=1,...,p$, do:
	*	Fit all $p\choose{k}$ models with exactly $k$ inputs
	* 	Out of all $p\choose{k}$ models, pick the one with the lowest training RSS, $M_k$

	Out of all $p+1$ models $M_0,...,M_p$, find the model that minimizes the cross-validated testing error
	
**Issue**: This algorithm requires analysis of $2^p$ models, which is prohibiting when $p$ is large.
*We are guaranteed to find the best model!*
**To overcome this issue, we can use forward or backward stepwise selection**

### Forward Stepwise Selection
**Algorithm**:
1. $M_0$ denotes the null model $\hat{y}=\hat{\beta}_0$ with no inputs
2. For $k=0,...,p-1$:
	1. Fit all $p-k$ models **that augment the model $M_k$ with one additional input**
	2. Out of all of these $p-k$ models, pick the one with the smallest training RSS, $M_{k+1}$
3. Out of the $p$ models $M_0,...,M_p$, find the model that minimizes the cross-validates *testing error*

*This algorithm is not guarateed to find the best model!*

### Backward Stepwise Selection
**Algorithm**:
1. $M_p$ denotes the full model $\hat{y}=\hat{\beta}_0+\hat{\beta}_1x_1+...+\hat{\beta_p}x_p$
2. For $k=p,p-1,...,1$:
	1. Fit all $k$ models that contain all but one of the inputs in the model $M_K$
	2. FOut of those $k$ models, pick the one with the smallest training RSS and call if $M_{k-1}$
3. Out of the $p$ models $M_0,...,M_p$, find the model that minimizes the cross-validated *test error*

*This algorithm is not guarateed to find the best model!*
