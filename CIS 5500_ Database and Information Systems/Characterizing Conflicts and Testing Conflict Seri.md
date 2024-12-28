We say two actions **conflict** if
* They are in different transactions
* They operate on the same data item
* At least one is a WRITE

We can have Read-Write, Write-Read, and Write-Write conflicts. If one were to swich two operations, if the value read/written is a different value in the second operation than it was in the first, it is a conflict.

### Testing Conflict Serializability 
To test for serializability, we construct a **precedence graph**, which is a graph $G(V,E)$ where the vertices $V$ are the transactions and the *directed* edges $E$ the conflicts between them. 
Recall there are 3 types of conflicts:
* READ-WRITE
* WRITE-READ
* WRITE-WRITE

If a *cycle* appears in the precedence graph, then the transactions are *not* serializable. If there is no cycle, then they are serializable, and the appropriate order of execution can be obtained from a **topological sort** of the precedence graph.

### "Undesirable" Phenomena
* We've characterized an execution as being "good" if it is serializable
* The **two-phase locking** theorem says that, if we use a well-formed and two-phase transactions combined with locking, then serializability is guaranteed.
* However, 2PL restricts the concurrency allowed in the system and may degrade performance
* Many systems therefore allow users to specify isolation levels for transactions, say which *undesirable phenomena* they can tolerate.
* If 2PL is not used, several undesirable phenomena may occur as a result of concurrency:
#### Dirty Reads
* Data that is written by an uncommitted transaction is called **dirty**; a **dirty read** is a read of dirty data by another transaction
	* This is an example if a WRITE $\rightarrow$ READ conflict
* Sometimes dirty reads are acceptable, sometimes they are not, it is context-dependent.
	* Concurrent deposit and withdrawal: dirty reads could lead to a negative balance. No constraint is violated.
	* Airline seat reservation: dirty reads may lead to the same seat booked tow two different people; this can be *compensated* by moving one passenger to another seat.

#### Unrepeatable Reads
* A transaction reads the same data item twice and gets *different values*
	* This is an example of a READ $\rightarrow$ WRITE conflict
* Sometimes unrepeatable reads are acceptable, sometimes they are not, it is context-dependent. After all, many times te purpose of querying a database twice is to get different results.

#### Overwriting uncommitted data
* One transaction overwrites the value of data hat is in the process of being written by another transaction
	* This is an example of a WRITE $\rightarrow$ WRITE conflict
* The "bad" concurrent deposit iis an example of this

#### Phantom Reads
* A transaction retrieves a collection of tuples twice but sees different results, even though it does not modify any of these tuples
	* The collection shares a common predicate, and insertions/deletions may be made on individual tuples in that collection by another transaction

*Many systems therefore allow users to specify **isolation levels** to define what underirable phenomena are permitted*