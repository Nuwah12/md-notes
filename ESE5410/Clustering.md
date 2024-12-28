## Clustering Problem
Find subgroups, or *clusters*, in datasets $D=\{\textbf{x}_i\}^N_{i=i}$

## K-Means Clustering
Given a dataset $D$, partition the set of subindices $\{1,...,N\}$ into $K$ subsets $C_1,...,C_k$ containing similar points
**Similarity Measures**: The *within cluster variation* (WCV) of cluster $C_k$ is defined by
$$\text{WCV}_k=\frac{1}{|C_k|}\sum_{i,j\in C_k}||x_i-x_j||^2$$
where $||x_i-x_j||$ is the *euclidean norm* between any pair of data points in the same cluster.
**Objective**: Find the subsets $C_1,...,C_k$ that minimize the sum of the WCVs. 
### K-means Algorithm
1. Initialize: Randomly assign a number $C(i)\isin\{1,...,K\}$ to each index (a.k.a data point) $\{1,...,N\}$
2. While cluster assignments change:
	1. For $k=1$ to $K$: (first loop sweeping all *clusters*)
		1. Compute the centroid of cluster $k$, defined as:
		$$\bar{c}_k=\frac{1}{|C_k|}\sum_{i\isin C_k}\textbf{x}_i$$
	2. For $i=1,...,N$: (second loop sweeping all *points*)
		1. $C(i) \larr\text{arg min}_k||\textbf{x}_i-\bar{c}_k||$ (assign each observation $i$ to tje cluster with the closest centroid)


* The value of the WCV decreases in each iteration
* However, the algorithm is *not guaranteed to give a global minmum*. Instead, we can find a good *local minimum*. What this means is that, for each random initialization of the centroids, the algorithm will most likely find different solutions for each one.
	* Thus, it is healthy to run K-Means several (4,5,6) times and select the run that produced the lowest overall error.

## Hierarchical Clustering
We will run an agglomerative process able to recursively generate a sequence of partitions with different numbers of groups, which can be plotted with a *dendrogram* (tree).
#### Main Idea
1. Start with each point being its own cluster
2. Identify the *closest* two clusters and merge them
3. Repeat until **all points are merged into a single cluster (agglomerative)**.

## Cluster Distance
We have several choices to measure the distance between two clu	sters of points $A$ and $B$:
* **Complete distance** Largest value among pairwise distances between points in clusters $A$ and $B$, i.e. $\text{max}_{\textbf{x}_i\isin A,\textbf{x}_j\isin B}||\textbf{x}_i-\textbf{x}_j||$
* **Single**: Smallest value among pairwise distances between points in clusters $A$ and $B$, i.e. $\text{min}_{\textbf{x}_i\isin A,\textbf{x}_j\isin B}||\textbf{x}_i-\textbf{x}_j||$
* **Average**: Average value of pairwise distances between points in clusters $A$ and $B$:
$$\frac{1}{|A|\cdot|B|}\sum_{\textbf{x}_i\isin A,\textbf{x}_j\isin B}||\textbf{x}_i-\textbf{x}_j||$$
* **Centroid**: Distance between the centroids of cluster $A$ and cluster $B$:
$$||\bar{c}_a-\bar{c}_b||, \text{where } \bar{c}_S=\frac{1}{|S|}\sum_{\textbf{x}_i\isin S}\textbf{x}_i$$
