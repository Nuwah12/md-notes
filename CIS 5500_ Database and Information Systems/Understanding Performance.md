### What Governs Performance?
* Speed of machine, of course
* Many software-controlled factors:
	* Caching and buffer management
	* How data is stored - physical layout, partitioning
	* Auxiliary structures - indexes
	* Locking and concurrency control
	* Different algorithms for oprtations - query execution
	* Different orderings for execution - query optimization
	* Reuse of materialized views, merging of query subexpressions - answering queries using viewsl multi-query optimization

### Cost of Accessing Data on Disk
* Time to access (read/write) a block:
	* *seek time* - moving arms to position the disk head on tthe track)
	* *rotation delay* - waiting for block to rotate under head
	* *transfer time* - actually moving data to/from disk surface
* The key to lowering I/O cost is to **reduce seek/rotation delays**.
	* Random I/O is more expensive than sequential I/O