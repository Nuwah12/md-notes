### GROUP BY
The syntax for `GROUP BY` is:
```
SELECT {group-attrs}, {aggregate-operator}(attr),...
FROM {list of relations}
WHERE {condition}
GROUP BY {group-attrs}
[HAVING {condition on aggregate}]
```
The intermediate query result calculated from the `FROM` and `WHERE` clause is grouped into sets of tuples that match over attributes specified in the `GROUP BY` clause. These attributes are referred to as the **grouping attrributes**.
In the `SELECT` clause, you can use one or more of these attributes, or an **aggregate operator** over one of the *non-grouping attributes*. The aggregate operator can be:
* `AVG`, `COUNT`, `SUM`, `MAX`, `MIN`
* If `DISTINCT` is used (inside the aggregate operator before the attribute name!), the bag over which the aggregate is computed becomes a set (duplicates are removed)

A common mistake is to use a non-grouping attribute in the `SELECT` clause without using an aggregate operator.
The `HAVING` clause eliminates groups from the final result.
