## Query API Calls
- query operation find items in a table based on the primary key attribute and a distinct value and returns all the attributes for that item
- use an optional sort key name and value to refine the results (ex. timestamp)
- by default the query will return all the attributes, but you can use the `ProjectionExpression` parameter to specify only specific attributes to return
- results always sorted by sort key 
  - if numeric, sorted in ascending order
  - if ASCII same thing, ascending order
  - can reverse the order by using the `ScanIndexForward` parameter to false
- by default all queries are eventually consistent
  - need to explicitly state if you want a query to be strongly consistent

## Scan API Calls
- scan operation examines every item in the table and by default it returns all data attributes
  - again use the `ProjectionExpression` to refine the scan to only return attributes you want

### Query or Scan?
- query is more efficient than a scan
  - a scan dumps the entire table THEN filters out the value to provide the desired result
  - adds an extra step of removing the data you don't want
  - as the table grows, scan operations can take longer 
  - a scan operation on a large table can use up the provisioned throughput in a single operation

### Improving Query Performance
- set a smaller page size (ex. return smaller number of items)
- running a larger number of small operations will allow other requests to succeed without throttling
- avoid using scan operations if you can
  - design tables in a way that you can use Query, GET, or `BatchGetItem` APIs

### Improving Scan Performance
- scan operations are sequential by default
  - returns 1MB increments before moving on to retrieve next 1MB
  - scans one partition at a time
- parallel scans is possible
  - you can configure DynamoDB to use parallel scans by logically dividing a table or index into segments and scanning each segment in parallel
- best to avoid parallel scans if your table is already incurring heavy read or write activity from other applications
- you can isolate scan operations to specific tables and segregate them from your mission-critical traffic
  - will require writing to two different tables

---
## Exam Tips: Scans vs Query
Scan: operation that examines every item in the table and by default will return all attributes
- use `ProjectionExpression` to refine results

Query: find items in a table using only the primary key attribute
- you provide the primary key name and a distinct value to search for
- results are always sorted by sort key in ascending order
- can set `ScanIndexForward` parameter false to reverse the order of your results

Performance
- reduce impact of your query or scan by
  - setting smaller page size which uses fewer read operations
  - isolating scan operations to specific tables
  - try out parallel scans
- a query operation is generally more efficient than a scan
- design tables in a way that you can use the Query, Get, or BatchGetItem APIs