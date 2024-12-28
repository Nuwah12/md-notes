Recall that to find the best query plan, the optimizer must be able to estimate the cost of a query plan
* Estimating the cost of a query plan is based on statistics that are maintained about the tables (refer to [Optimizing Queries](../CIS%205500_%20Database%20and%20Information%20Systems/Optimizing%20Queries.md))
* At each point in a wuery plan, the intermediate result size (*cardinality*) is estimated based on these statistics.
* The total cost of the query is calculated using the estimated result size at each point in the query plan

To estimate the cardinality of a result at each step
* Calculate the **reduction factor** of the predicate for a select expression (also called **selectivity**)
* Understand any key/foreign key relationship betweem the relations being joined

### Estimating Reduction Factor for Selections
* The reduction factor of a predicate, $\text{RF}(c)$, is the ratio of the expected result size to the input size due to $c$. This can be estimated as follows:
	* attr = value: 1/(num distinct values in attr)
	* attr1 = attr2: 1/(MAX(num distinct values in attr1, num distinct values in attr2))
	* attr > value: (HIGH(attr)-value)/(HIGH(attr)-LOW(attr))
* If there are k predicates in the eselection over R, independence is assumed and the cardinality of the result is estimated as: NTuples(R) * (RF(c1) * RF(c2) * ... * RF(ck))

### Estimating Reduction Factor for Joins
* For a join $R \bowtie_\theta S$ (R JOIN S ON theta), if there is a key-foreign key relationship from R to S expressed in $\theta$, the cardinality of the join result is NTuples(R)
* Otherwise, the cardinality of $R \bowtie_\theta S$ is NTuples(R) * NTuples(S) * RF($\theta$)

### Estimating the number of results pages
* For blocking operators, te system also calculates the number of result pages as:
	$\lceil\text{cardinality}/\lfloor(\text{page size)}/(\text{result tuple size})\rfloor\rceil$