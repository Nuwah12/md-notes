## Nested Loops Join: $R\bowtie_\theta S$
```
for each page of tuples in R do
	for each page of tuples in S do
		// compare r in page of R with s in page of S
		if ri == sj then add <r, s> to result 
```
* We should choose the *smaller relation* for the outer loop! This will guarantee fewer I/Os.
* **Algorithm**: For each page of R, get each page of S. Write out matching pairs of tuples `<r,s>` to an output buffer
* **Cost**: $M+M\times N$, where $M$ and $N$ are the number of pages in the relations

## Block Nested Loop Join
```
until all of R has been read {
	read in B-2 pages of R
	for each page of tuples in S {
		Read in a single S page
		// compare each r on a buffered R page with s on a buffered S page
		if ri == sj then add <r, s> to result
	}
}
```
* **Algorithm**:
	* One page is assigned to be the output buffer
	* One page is assigned to be the input from S, **B-2 pages assigned to input from R**
	* Compare all tuples on buffered pages and output matches
*  **Cost**: $M+\lceil \frac{M}{B-2}\rceil\times N$, where $M$ is the size in pages of the smaller relation, $N$ the larger, and $B$ the number of buffers used
*  Again, the *smaller relation should be used in the outer loop*.

## Index Nested Loops Join
```
for each tuple r on a buffered page in R do {
	for each tuple s in S where ri == sj do {
		add <r, s> to result
	}
}
```
* Each page of the outer relation *is read only once*
* **Algorithm**:
	* One page is assigned to be the putput buffer
	* One page is assigned to input from R, one page for matching S page
	* Use index on the search key sj to get matching s tuple(s) and output all such  `<r, s>`
* **Cost**: $M+((M\times p_R) \times \text{cost of finding matching S tuples})$
	* $p_R=$ number of tuples per page
* The relattion with the smallest number of BLOCKS should be used as the outer relation! 

## Hash Join
* Basic idea is to divide and conquer 
* **Pass 0**: Partition both relations using hash function $h$: $R$ tuples in partition $i$ will only match $S$ tuples in partition $i$
* **Pass 1**: Read in a partition of $R$. Scan the matching partition of $S$, and search for matches.
* Conditions to use Hash join
	* Number of partions must be less than $B-1$, because in pass 0 the relation is partitioned by scanning the relation using 1 buffer
	* Size of largest partition in smallest relation must be less than $B-2$, beacuse in pass 1 an R partition must be completely placed in buffered memory
	* $B$ must be greater than $\sqrt{M}$ (size of smaller relation)
* **Cost**: 
	* Pass 0: Cost to partition R = 2M, cost to partition S = 2N
	* Pass 1: Cost to join partitions = M+N, cost of writing the output is not counted
	* Total cost = $3\times (M+N)$