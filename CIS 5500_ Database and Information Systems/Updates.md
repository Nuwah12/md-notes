* Tuples can be inserted explicitly into the database:

```
INSERT INTO professor (fid, name)
VALUES (4, 'Simpson')
```

* We can insert the results of a query:

```
INSERT INTO professor (fid, name)
	SELECT sid AS fid, name
	FROM student
	WHERE sid < 20
```

* Tuples may be deleted or updated:

```
DELETE
FROM student s
WHERE s.sid < 25
```
```
UPDATE student s
SET s.sid = 2 + s.sid, s.name = 'Boon'
WHERE s.name = 'Bo'
```

**Modifying Scema**
* Alter table to add columns, we must specify a type and a default value:

```
ALTER TABLE student
ADD gpa real NULL
```
Here we add a column called gpa that is of type real and its default value (the value it will be filled with) is NULL.

Some, but not all, systems will allow columns to be dropped:
```
ALTER TABLE student
DROP COLUMN gpa
```

It is also possible to change the column type:
```
ALTER TABLE student
MODIFY COLUMN gpa decimal
```
Here we change the type of column gpa to decimal.

**Adding/Dropping Constraints**
* A primary key or other named constrasint may be added:

```
ALTER TABLE student
ADD CONTRAINT std_pk PRIMARY KEY (sid)
```

* It can also be dropped:

```
ALTER TABLE student
DROP CONSTRAINT std_pk
```

**DROP command**
We can drop both tables and views from the database by stating `DROP {name}`.