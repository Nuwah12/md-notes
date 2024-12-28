A **database management system (DBMS)** is a software package designed to store and manage databases
* Reliable storage and recovery of 100s of GB of data
* Querying/updating interface and API for apps and web pages
* Support for many concurrent users

#### Benefit 1: Generality and Declarativity
* The user does not need to understand details like indexes, sort orders, machine speeds, disk speeds, concurrency, etc.
* Instead, the user programs with a *logical model* in mind
	* "Give me all appointments on 10/28" rather than "loop over all events and return those with a data of 10/28". (*What we want* vs. *How to get it*)
		* The user does  not need to be aware of the *implementation* of the return process, i.e. the search algorithm being used to look through the data upon a query.

#### Benefit 2: Efficiency and Scale
* Queries are executed quickly, and this is true for databases with hudreds of entries and those with hundreds of thousands of entries. 
* The queries the user writes will remain unchanged, yet the implementation of these queries may be changed to make them quicker.

### Benefit 3: Magament of Concurrency, Consistency, and Reliability
* Suppose other people are allowed to access the database and are allowed to modify it. How do we keep things consistent? What if someone makes an update on a disconnected machine? What if the system crashes while we are changing the database, how do we recover our work?2
* We specify the format of our database as tables and constrains
* Then need to to "physical" design: layout on disk, indexes, etc.
* Structured Query Language (SQL) is often embedded, e.g. in Java or Javascript
	* Based on **restricted first-order logic expressions** over relations
	* Not procedural - defines contraints on the output
	* Is **declaritive** - meaning we specify data we want, not how to get it
* Converted into a query plan and executed using the query optimizer and query execution engine

**Example: Processing the Query:**
The SQL query is passed to the DBMS query optimizer, which produces a query plan. The query plan is a tree whose nodes specify how the operator is to be executed by the engine.
The query plan is passed to the execution engine, and the result is served to the requesting application.