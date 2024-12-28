The **key** of a table is a subset of attreibutes of a table that uniquely identifies the tuple, that is all instances of the key attribute are unique.
A key may consist of one or more columns, such that they form unique identifiers for eacg tuple in the table.

A key in one table may be referenced by another table by what is called a **foreign key**, in other words a foreighn key references a key. If this constraint is enforced (i.e. we can't have foreign leys that do not exist in the key column) we have ***referential integrity***.
Foreign keys may be part of the key for the referring table.

### Constraints, Keys and Foreign Keys
Remember that a Key for a table/relation can be a combination of columns. How can we determine which attributes are the Keys for a given relation?
* We can eliminate sets of attributes that *cannot* be keys by looking at an instance of a relation; i.e. names, values (i.e. money)
* To understand possible Keys, schema (i.e. column names and table name) are helpful
* Ultimately, it is a demantic assertion about what the data is meant to represent

*Names of foreign Keys do not need to be the same as the attibutes (Keys) they are referencing!*

For many-to-many relations between to tables/relations, an additional "all-key" table must be introduced to 