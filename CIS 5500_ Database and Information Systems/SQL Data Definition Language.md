### SQL: Structured Query Language
* THE standard language for relational data
	* Invented by Don Chamberlin et al. at IBM
* There have been a series of SQL standards
* Separated into a **DML** (Data Manipulation Language) and **DDL** (Data Definition Language)
	* DML is based on relational algebra and calculus

#### DDL Specifies the database schema
* The tables, with a name for each table
* The attributes for each table and the domain (vlaue range) for each attribute
	* Includes the data type of the attribute
* The key(s) for each table
	* There can be more than one key for a table. One is chosen as PRIMARY LEY, and the others are "alternate" keys and are indicated using the keyword UNIQUE
* All appropriate foreign keys

**Specifying Schema in SQL DDL**
```
CREATE TABLE Account (
	number	INT,
	owner	VARCHAR(30),
	balance	DECIMAL(19,2),
	type	ENUM('checking','savings'),
	PRIMARY KEY (number))
	
CREATE TABLE Check (
	acct_no	INT,
	check_number	INT,
	date	DATE,
	amount	DECIMAL(19,2),
	PRIMARY KEY (account_no, check_number) # more than one primary key here
	FOREIGN KEY acct_no REFERENCES Account (number)) 
```
We can insert rows into the table once they are created. We must ensure that the attribute being referenced by a foreign key exists before a row with that foreign key is added! This is **referential integrity**:
```
INSERT VALUES INTO Account
VALUES	(101, 'J. Smith', 10000, 'checking'),
		...
		
INSERT VALUES INTO Check
VALUES	(101, 924, '2000-10-23', 125),
		...
```