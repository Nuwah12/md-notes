**Embedded SQL** is SQL written inline with an application's source code.
* The applicationis written in a *host programming language*, i.e. JavaScript, Java, Python
* Allows data from a database to be accessed within a program
* Requires a library/driver to provide language-specific statements/functions for the four basic SQL actions:
	* Connecting to a database
	* Executing a query
	* Accxessing query results
	* Closing database connection
* Can use the values of the host variables at runtime to generate **dynamic queries**.

**Cursors** are control structures that enable controlled traversal over records in a (resulting) table
* The need for cursors arrises from the fact that we don't have any *a priori* knowledge about the size of the query result. Therefore, we cannot accurately allocate memory for the query result.