We can designate a special "null" value to represent an "unknown" or "not applicable"/NA value. In SQL, this value is denoted as `NULL`.
### Three-State Logic
* We need a way to evaluate Boolean expression and have the result be True, False, or Unknown
* We must define logical expressions AND, OR, and NOT with these 3 values:

**AND**:
* T AND T = T
* T AND U = F
* T AND U = U
* U AND U = U

**OR**:
* T OR T/U = T
* F OR F = F
* F OR U = U
* U OR U = U

**NOT**:
* NOT F = T
* NOT T = F
* NOT U = U

Another way of thinking about three-state logic is assigning numbers to each value, where $T=1$, $F=0$, and $U=0.5$. To calculate the logical values, we can follow simple riles after assigning these values:
* **AND**: calculate `MIN(X,Y)`
* **OR**: calculate `MAX(X,Y)`
* **NOT**: calculate $1-X$

Finally, we need rules for `NULL` values in arithmetic and aggregation.
* If `NULL` appears in a comparison, then the result is UNKNOWN
	* E.g. if `x=NULL`, the truth value of `x=="Joe"` would be `UNKNOWN` 
* If `NULL` appears in an arithmetic expression, the result is `NULL`
* `NULL` values are ignored in an aggregation, except for `COUNT(*)`
	* E.g. `MAX` will drop all `NULL`s and calculate the max, if all values are `NULL` then result is `NULL`
	* `COUNT` counts all tuples, even ones that include only `NULL`
* `NULL` compared with anything, including `NULL`, is `NULL`.

In the final result of a query, only tuples yielding TRUE value are returned, i.e. FALSE and UNKNOWN tuples are dropped.
An explicit test for `NULL` exists in SQL, and is done with `IS NULL`.

**NULL in GROUP BY**:
* `GROUP BY` treates all `NULL`s as equal, so tuples with `NULL` are grouped together

**NULL in Set Operations**:
* Without using `ALL`, `NULL` values are all treated as equal. With `ALL`, all individual `NULL`s are retained.

**SQL DDL and NULL Values**:
* By default, any column can hold `NULL` values, *except for Primary Key columns*.
* To disallow `NULL` in a column, use `NOT NULL` when the column in the table is created