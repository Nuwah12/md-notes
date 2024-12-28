* DBMS performance is affected by many factors
	* Locking and concurrency control (specified by isolation levels)
	* How the data is stored
	* Auxillary structures (i.e. indexes)
	* Different algorithms for operations (query execution)
	* Different orderings for execution (query optimization)
	* Reuse of materialized views, merging of query subexpressions (multi-query optimization)

## Codd's Logical Operators: Relational Algebra
* There are 6 basic operators:
	* Projection $\pi_\alpha(R)$
		* i.e. SELECT
	* Selection $\sigma_\theta(R)$
		* i.e. WHERE
	* Rename $\rho_{\alpha\rightarrow\beta}(R)$
		* i.e. AS in SELECT
	* Union $R_1 \cup R_2$
	* Difference $R_1-R_2$
	* Product $R_1 \times R_2$
* Projection, Selection, and Rename are **Unary operators**, as they operate on 1 relation. The other three are **binary**.

We will also use the join operator $\bowtie_\theta$, i.e. $R_1\bowtie_\theta R_2$