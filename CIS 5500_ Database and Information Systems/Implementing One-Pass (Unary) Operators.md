### Table Scan
* Sequential scan: read through all pages of table
* Index scan: retrieve tuples by scanning the data entries
	* This retrieves in index order, which may be useful
	* Recall that in Alternatives 2 or 4, the data entry is not the datam therefore this may require 1 page I/O per tuple when the index is unclustered
	* Cost: b(T) pages for sequential scan
	* Clustered index: i(T)+b(T)
	* Unclustered index: up to i(T)+r(T)

#### SELECT ($\sigma_\theta$)
* If unsorted and no index, scan the file and check each tuple against predicate $\theta$. Cost is $b(T)$
* If sorted data, equality/range search applicable, no index:
	* Binary search, cost is $\log_2b(T)$ to find first page, then # pages with matching tuples
* If indexed, apply $\theta$ to index if possible
	* If predicate is a conjuction:
		* If multiple indexes match different terms of perdicate, then use intersection of index data entry results
		* Retrieve tuples, and use scanning loop to test terms not matched by any index
	* If perdicate is a disjunction:
		* If multiple indexes match different terms of predicate, then use union of index data entry results
		* Retrieve tuples, and use scanning loop to test terms not matched by index
	* Cost: cost of using indexes (# of I/Os), then # pages with matching tuples

#### PROJECT ($\Pi_\alpha$)
* Simple scanning method is:
```
while more tuples
	read tuple
	output attribute in alpha
```
* Duplicate removal may be required (i.e. SELECT DISTINCT)
	* Hash-partition output into separate files by bucket, do duplicate removal on those (if smaller no. of duplicates)
	* If have many duplicates, sorting may be better 
* Cost: cost of scanning + cost of duplicate removal