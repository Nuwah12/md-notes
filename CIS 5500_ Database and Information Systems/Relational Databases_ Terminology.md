### Table Structure
Relations can be presented as tables, with columns representing *attributes* and rows representing individual data instances.
Each table is *named*, and contains a fixed number of *columns/attributes*. The name and attributes of the table are what we call the ***schema***, which defines the structure of the table (i.e. it is the *definition* of the table). The schema may change *slowly* over time, as new information about data instances needs to be captured.
Each entry in the data is called a *row* or ***tuple*** (other times a *record*). The number of rows in the table generally changes more rapidly, as new data is constantly being generated.
An ***instance*** of the table is the current state of the table's row values. The schema is the ***intension*** of the table, and the rows are the ***extension*** of the table.
**To Summarize**: The schema, intention, defines the information in the real world we would like to capture. The instance, extension, is the current state of the information in the real world.

#### 'Dimensions' of a Table
*Degree* or *arity* of a table is the number of columns.
*Cardinality* of a table is the number of rows in the current instance.

A relational database consists of many, interconnected tables.
