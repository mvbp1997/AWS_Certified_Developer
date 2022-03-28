## DyanmoDB Indexes
- a secondary index allows you to perform more flexible query
- query based on an attribute that is not the primary key
  - using global secondary indexes and local secondary indexes
- a secondary index allows you to perform fast queries on specific columns in a table
  - select columns you want included in the index and run your search on the index 
  - this is more performant because you query the index columns only rather than the entire dataset

### Local Secondary Index
- index that can only be created when creating your table
- primary key = partition key of table + a different sort key
- allows you to have a different view of your data, organizing according to an alternative sort key
- any queries based on this sort key are much faster using the index rather than the main table
- only limitation is that it can only be added during creation of the table (cannot add, remove, modify later)

### Global Secondary Index
- can create whenever you like
- different partition key and sort key, fast queries on this index
- gives a completely different view of the data

--- 
## Exam Tips: Secondary Indexes
- enable fast queries on specific data columns
- provide a different view of the data based on alternative partition and sort key
- Local Secondary Index: same partition key and different sort key to your table; can only be created when you create a table
- Global Secondary Index: different partition key and different sort key to your table; can be created at any time