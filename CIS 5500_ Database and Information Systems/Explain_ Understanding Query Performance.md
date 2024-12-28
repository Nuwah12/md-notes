## EXPLAIN
* EXPLAIN is a profiling tool that shows how your query will be executed. It shows the **query plan** with *estimates* of the number of rows and time spent at each  operation in the plan.
* The plan can be visualized *inline* or *graphically as a tree*

The query plan produced by EXPLAIN can reveal issues in the SQL query, such as
* Unnesessary use of a table
* Unintentional cartesian product (rather than join) (`SELECT .. FROM r1, r2` does a cartesian product)

It can also show very large intermediate results that could be made smaller by:
* Introducing useful indexes to retrieve only matching rows
* Eliminating unnecessary columns (i.e. is `SELECT *` really needed?)

## Tips for writing better queries
* Make sure the query is correct and succint
	* Only include necessary tables
	* Only return necessary columns
* Look for phrase "Cartesian Join" in the query plan, chances are it is unintended
	* Use `JOIN..ON` to avoid missing join conditions (JOIN without ON clause will throw error)
	* Avoid CROSS JOIN unless absolutely necessary
* Look for unused compound indexes
	* I.e., an index on (country, city) and the query specifies just a city, because it is "understood" that the country is USA.