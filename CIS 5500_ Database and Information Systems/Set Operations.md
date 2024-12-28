A **set** contains no duplicate items, e.g. $\{1,2,5\}$.
A **bag** (a.k.a. **multiset**) may contaion multiple copies of the same element, e.g. $\{1,1,2,5,5,5\}$.

We can ensure our queries return a proper *set* by using the `DISTINCT` keyword. One reason we may not use this and opt for the default bag-behavior is that selecting distinct items requires sorting or caching. Also, the multiplicity of an element may tell you something useful.

### Set Operations in SQL
* Set operations default to set semantics, not bag semantics:
```
(SELECT..FROM..WHERE)
{op}
(SELECT..FROM..WHERE)
```
Where `{op}` is one of:
* `UNION`
* `INTERSECT`
* `MINUS`/`EXCEPT` - many DBs don't support this

We use `ALL` for bag semantics. Using set operations with the `ALL` keyword after them *removes duplicates, as is set behavior*. This query will return the duplicates that are a reuslt of the union:
```
(SELECT name FROM student)
UNION ALL
(SELECT name FROM Professor)
```
A UNION can be performed by `JOIN..ON`:
```
SELECT DISTINCT dis
FROM students s JOIN Takes t ON s.sid = t.sid
```
`INTERSECT` can be expressed using `MINUS` as:
$$R \cap S=R-(R-S)$$