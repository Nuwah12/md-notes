Recall that the 'I' in the **ACID** properties stands for *Isolation*.
* Isolation means that each transaction must appear to execute without interference from others concurrently executing transactions.
* *Why is this hard?*

### Serial Execution
One transaction is completely executed, followed by the second transaction.

### Interleaved Execution
In an interleaved execution the actions of concurrent transactions are intervleaved one after the other. This is desirable to increase response time.

* Some interleaved executions are bad/incorrect (class deposit example)
* Can also be completely fine, i.e. deposits to two completely separate accounts.

### Good Executions, i.e. guarantee isolation
An execution is good if it is serial or serializable (i.e. equivalent to some serial execution).