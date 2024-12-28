**Objective**: Consider a collection of $p$ input variables $X_1,...,X_p$, find a smaller number $M<p$ of artificial input variables, $Z_1,...,Z_m$, related to the original variables via *linear combinations*.
$$Z_m=\phi_{m1}X_1+\phi_{m2}X_2+...+\phi_{mp}X_p$$
$$=\Phi^T_m\bf{X}$$
, that is, the artificial variable $Z_m$ is related to the input data $\bf{X}$ via some vector of coefficients $\Phi_m$.
**PCA Criterion**: Find a linear combination of input variables that have *maximal variance* and are *mutually uncorrelated*. This criterion is identical to the one use in PCR.
* *Variance*: We proved that $\text{Var}[Z_m]=\Phi_m^T\Sigma_X\Phi_m$, where $\Sigma_X$ is the covariance matrix and is equal to $\text{E}[(\bf{X}-\mu_X)\cdot(\bf{X}-\mu_x)^T]$.
* *Mutually uncorrelated*: Two r.v.'s $Z_i$ and $Z_j$ are uncorrelated if $\Phi_i^T\Phi_j=0$, that is, their coefficient vectors are orthogonal and their dot product is zero. We are essentially forcing the variables to explore 'new directions'.

To find the vectors $\Phi,...,\Phi_m$ that satisfy these conditions for data, we *maximize* the following expression over all $\Phi_m$
$$\text{max}\sum_{m=1}^M\Phi_m^T\Sigma_X\Phi_m$$
such that $||\Phi_i||=1$ for all $i$, and $\Phi_i^T\Phi_j=0$ for all pairs $(i,j)$.
**Solution**: The unit-length eigenvector of $\Sigma_X$ corresponding to its $m$-th largest eigenvalue $\lambda_m$. The vectors $\Phi_m$ are called the **principle components**.
**To generate a dimensionally-reduced point**, we take the first $p$ eigenvectors (when we are reducing to dimension $p$), and stack them as columns into a matrix. Then matrix multiply with the (transposed) data matrix to find the new data point.

**Standardization**: Before doing PCA or PCR, you should *standardize* the input variables, i.e.
$$\tilde{X}_i=\frac{X_i - \bar{X}_i}{\tilde{\sigma}_i}$$
, where $\bar{X}_i$ and $\tilde{\sigma}_i$ are the empirical mean and standard deviation of the $i$-th input variable. Then, apply PCA with these standardized variables $\tilde{X}_i$.
By doing standardization, we obtain a more 'spherical' cloud of points, where the variances are more pronounced in either dimension.

### Proportion of Variance
Since the variances of each individual variable $X_1,...,X_p$ are given on the diagonal of the covariance matrix $\Sigma_X$, the total variance in the dataset is given by $\sum_{j=1}^p=\text{Var}[X_j]=\text{Trace}(\Sigma_X)=\sum_{i=1}^p\lambda_i$

The variance of the $m$th principle component is $\text{Var}[Z_m]=\lambda_m$, that is, the variance *explained by the $m$-th artificial input*, is equal to the eigenvalue associated with the $m$-th principle component - the larger the value of $\lambda_m$, the larger the variance of the $m$-th artificial inpit $Z_m$ - it contains more information.

The **Proportion of Variance Explained** (PVE) of the $m$-th principle component is
$$\text{PVE}_m=\frac{\lambda_m}{\sum_{i=1}^p\lambda_i}=\frac{\text{Var}[Z_m]}{\sum_{j=1}^p\text{Var}[X_j]}$$

You can plot both the proportion of variance explained per principle component, and the cumulative proportion of the variance explained by each component, which is monotonically increasing to one.
In the proportion of variance explained plot, the elbow usually indicates a good place to truncate the principle components, i.e. any more transformations beyond that point will not be helpful. **The height of each point, i.e. its y component (proportion of variance), is proportional to the corresponding eigenvalue**.