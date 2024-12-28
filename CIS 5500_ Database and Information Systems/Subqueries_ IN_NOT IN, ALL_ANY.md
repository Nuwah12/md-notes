### Subqueries
* A subquery can occur in the `WHERE` clause of a query
	* **Uncorrelated**: independent of outer query
	```
	SELECT sid
	FROM Takes
	WHERE cid IN
		(SELECT cid
		 FROM Takes
		 WHERE sid=1)
	```
	* **Correlated**: refers to variables in the outer query
```
SELECT sid, name
FROM Student s
WHERE EXISTS
	(SELECT t.sid
	 FROM Takes t
	 WHERE s.sid = t.sid)
```
This means that the subquery must be considered for *every tuple in the outer scope*.

### IN/NOT IN
`IN` tests for membership of a value in a set of values
`NOT IN` tests for non-membership of a value in a set of values

### ANY/ALL
`ALL` is used for *universal quantification* , i.e., True or False is returned for each tuple in the outer query if *all* tuples in the subquery fulfill some logical condition.
`ANY` is used for *existential quantification*, i.e., True or False is returned for each tuple in the outer query if *any* of the tuples in the subquery fulfill some logical condition.