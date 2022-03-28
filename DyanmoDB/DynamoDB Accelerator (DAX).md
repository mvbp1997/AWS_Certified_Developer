## What is DAX?
- DynamoDB Accelerator is a fully managed, clustered in-memory cache for DynamoDB
- increase read performance (10x)
- microsecond performance for millions of requests per second 
- ideal for read-heavy and bursty workloads (ex. auctions, gaming, retails, etc.)

### How Does it Work?
- DAX is a write-through caching service
- data is written/updated to the cache and the backend store at the same time
- allows you to point your DynamoDB API calls to DAX cluster
  - query DAX cluster first before the backend store
- cache hits on the DAX return immediately
- cache misses on the DAX will prompt it to perform an eventually consistent read request from DynamoDB into the DAX then returns 

### Benefits
- retrieval from DAX instead of DynamoDB reduces the read load on backend store
- may be able to reduce provisioned read capacity

### Not Suitable
- caters mostly for eventually consistent reads
- not gonna work for apps that require strongly consistent reads
- not suitable for writing-intensive applications
- not suitable for apps that don't do that many rad operations
- not suitable apps that do not require microsecond response time

---
## Exam Tips
- Provides in-memory cache for DynamoDB Tables
- improves response times for eventually consistent reads only
- data is written to the cache and the backend store at the same time
- point your API calls to the DAX cluster instead of your table
- cache hits = DAX returns immediately
- not suitable for write-intensive apps or apps that require strongly consistent reads

---
## Time-To-Live (TTL)
- attribute that describes the expiry time for your data
- expired items are marked for deletion
- once marked, items are removed after 48 hours
- great for removing irrelevant or old data (ex. session data, event logs, etc.)
- helps to reduce costs of your table 
- TTL is expressed in the Epoch time format
