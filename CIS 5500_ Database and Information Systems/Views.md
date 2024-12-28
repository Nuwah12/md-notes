Views are named queries that can be used in other queries. We define a view using the `CREATE VIEW` command, e.g.:
```
CREATE VIEW Top_Students(sid,sname,gpa) AS
	...
```
note that we define the name and schema of the view. Each time the view is referenced from another query, the view definition is substituted for the name, i.e,. it is **computed upon request**, unlike a temporary table, whose result is computed once and then stored for later use.
*A view always reflects the current state of the database*.
### Why are views useful?
* like temp. tables and CTEs, they simplify complex querues
* View facilitate security/access control
	* Different user groups can see different views of the database
	* We can assign user permissions on views
* Views can be used in query optimization
	* If materialized, i.e. stored and updated as the database changes
* Views can be used to describe transformations or mappings from one sceha to another
	* Basis of converting between different data models or representations
	* Useful for logical data independence

### Views can be materialized
* Materialized views are important for query optimization
* A **materizlized view** is computed once and its results are stored as a table, as opposed to a **virtual view**.
	* BUT, it *must be updated as the underlying database changes*

We can create a materialized view using `CREATE MATERIALIZED VIEW`

### Updating the Database Through Views
* Some views can be updated, and the changes propogated to the base relations
* A view is updatable if:
	* It is defined ona single base table
	* It uses only selection and projection
	* There are no aggregates
	* `DISTINCT` is not used