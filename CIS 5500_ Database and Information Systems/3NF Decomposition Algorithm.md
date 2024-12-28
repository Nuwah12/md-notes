```
Let F be a minimal cover, R be a non-3NF schema
i := 0
for each FD X --> Y in F {
	if none of the schemas Rj, 1 <= j <= i, contains XY {
		increment i
		Ri := (X, Y)
	}
}
if no schema Rj, i <= j <= i contains a candidate key for R {
	increment i
	R := any candidate key for R
OPTIONAL: combine all Ri's which have the same key
}
return (R1, ..., Ri)
```

In step 1, we output schemas for each functional dependency, such that the attributes in this new schema are not a subset of any of the previously generated schema.
In step 2, we check to see if a candidate key for R is included in one of the newly generated schema. If yes, we move on. If no, we also include a schema for the key.
In step 3, we can optionally combine all of the new relation that have the same key.

The decomposition is guaranteed to have a lossless join and preserve dependencies.