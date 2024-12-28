### SQL Update Language
We've discussed how to create relational schema using the Data Definition Language (DDL), as well as how to insert rows using `INSERT TO <table_name> VALUES ...`
You can update one or more rows of a table using:
```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
Rows cal be deleted via `DELETE FROM <table_name> WHERE condition;`

### Actions and Transactions
* Updates translate into `READ(x)` and `WRITE(x)` **actions** on the database instance, where `x` is a **data item**.
	* Typically a data item is a row in a table (tuple), but it could be a table or subset of a table.
* Actions are bundled into a unit of work called a **transaction**
	* If the transaction succeeds, the effects of all write operations persist (**commit**), it it fails, no effects persist (**abort**)
	* These guarantees are made despite concurrent activity in the system, and despite failures that may occur

#### From SQL to Actions
* Suppose we have a table of bank accounts which contains the account number and balance of each account 
* A deposit of $50 to account # 1234 would be written in SQL as:
```
UPDATE Accounts
SET balance = balance + 50
WHERE account#= '1234';
```
* This is translated into the following, where X is the data item representing the tuple in accounts ({...} is a comment):
```
READ(X.bal)
{X.bal := X.bal + 50}
WRITE(X.bal)
```

Transactions can be specified between `BEGIN TRANSACTION;` and `COMMIT;` statements.

### Rollback
* Most systems allow intermediate savepoints to be specified in the transaction, and for the transaction to ROLLBACK to a specified savepoint.
	* This removes the effect of any WRITE operations performed since the savepoint
	* An abort means hat the ROLLBACK is to the beginning of the transaction
* A transaction may abort either because the programmer decides to do so, or because the system forces it
	* Constraint violations, e.g. the balance of an account must be > 0
	* Failures
	* Managing concurrency in the system
* If the transaction aborts for any reason, any writes that it performs must be "not seen" in the database state

### ACID Properties of Transactions
* **Atomicity**: Either all of the actions (read/write) of a transaction are executed, or none are
* **Consistency**: Each transaction executed in isolation keeps the database in a consistent state
* **Isolation**: Transactions are isolated from the effects of other, concurrently executing, transactions
* **Durability**: Updates persist in the DBMS