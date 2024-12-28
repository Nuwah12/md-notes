1. **Reflexivity** - if Y is a subset of X, then X must functionally determine Y, also called *trivial dependeicies*, since we don't need any functional dependencies, just a schema.
2. **Augmentation** - If **X --> Y**, then **XW --> YW**. That is, if we have an FD, both sides can be augmented with some other attribute. **XW** and **YW** refer to the union between the sets **X/Y** and **W**.
3. **Transitivity** - If **X --> Y** and **Y --> Z**, then **X --> Z**.

### Consequences of Armstrong's axioms
1. **Union**
If **X --> Y** and **X --> Z**, then **X --> YZ**.
Proof:
* Since **X --> Y** then by *augmentation by X*, **XX --> XY**, which is just **X --> XY**
* Since **X --> Z** then by *augmentation by Y*, **XY --> YZ**
* Since **X --> XY** and **XY --> YZ**, then by *transitivity* **X --> YZ**

2. **Decomposition**
If **X --> Y** and **Z $\subseteq$ Y** then **X--> Z**
Proof:
* Since **Z $\subseteq$ Y** then by *reflexivity* **Y --> Z**
* Since **X --> Y** and **Y --> Z** then by *transitivity* **X --> Z**

By decomposition, we can say that **AB --> DE** can be decomposed into **AB --> D** and **AB --> E**

Armstrong's Axoims can be proven to be **sound** and **complete**:
* ***Sound***: any relation satisfying FDs in F will satisfy those derivable from F using Armstrong's Axioms
* ***Complete***: If an FD **X --> Y** cannot be derived by Armstrong's axioms from F, then there exists some relational instance satisfying F but not **X --> Y**.

Armstrong's axiums derive *all* the FDs that should hold