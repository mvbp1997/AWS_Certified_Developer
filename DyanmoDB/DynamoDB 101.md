## Introduction to DynamoDB
- fast and flexible NoSQL database 
- good for data that needs to be consistent, single-digit millisecond latency
- supports key-value data models; supported document formats are JSON, HTML, XML
- great fit for mobile, web, gaming, and other apps
- is a serverless tech; integrates well with lambda
- can be configured to automatically scale

### DynamoDB Features
- High Performance: SSD storage
- Resilience: avoid single point of failure; spread across 3 geographically distinct data centers
- Consistency: eventually consistent reads (default) and strongly consistent reads 

### Consistency Models
Eventually Consistent Reads
- consistency across all copies of data is usually reached within a second 
- (best for read performance)

Strongly Consistent Reads
- read always reflects successful writes; writes are reflected across all 3 locations at once 
- (best for read consistency)

ACID Transactions
- DynamoDB Transactions provide the ability to perform ACID (Atomic, Consistent, Isolated, Durable) transactions
- Atomic: all or nothing
- Consistent: consistent with data validation rules
- Isolated: transactions must happen in isolation, not impacting other transactions
- Durable: data must be resilient 
- read/write multiple items across multiple tables as an all or nothing operation

### DynamoDB Definitions
- items = records in a table (row) 
- attributes = column of data (column)
- key = name of data
- value = data itself lol

### Primary Keys
- primary keys allow us to query the table
- DynamoDB stores and retrieves data based on a primary key
- Two Types: Partition Key & Composition Key (partition key + sort key)
- Partition Key: a unique attribute of an item (customerId, emailAddress, etc.)
  - value of partition key is input to an internal hash function which determines the partition or physical location on which the data is stored 
  - no two items can have the same partition key
- Composite Key: partition key + sort key
  - use when partition key is not necessarily unique 
  - ex. Forum Posts where users post multiple messages (combination of userId + timestamp) 
  - items in the table may have the same partition key, but they must have a unique combination of sort key
  - all items with the same partition key are stored together and then sorted according to the sort key

---
## Exam Tips: DynamoDB
- DynamoDB is a low latency NoSQL database
- supports both document (JSON, HTML, and XML) and key-value data models
- Consistency Models
  - Eventually Consistent (default): overall read performance is better, can take up to one second from write to read
  - Strongly Consistent: all writes immediately take effect in all 3 physical locations 
- DynamoDB supports ACID transactions
  - think about making a credit card payment (all-or-nothing)
- DynamoDB features consists of tables, items, and attributes
- 2 Types of Primary Keys
  - Partition: unique attribute of an item
  - Composite Key: partition key + sort key (unique combination of attributes for an item)

---
## DynamoDB Demo
- IAM user with DynamoDB access (dynamo-admin)

---
## Controlling Access to DynamoDB
IAM: Authentication and access control is managed through AWS IAM
- create IAM users with specific permissions to access and create DynamoDB tables
- can also create IAM roles to enable temporary access to DynamoDB 
- to restrict a users access, use IAM condition in the policy to restrict a user to only their own records 

---
## Exam Tips: DynamoDB Access Control
- you can configure fine-grained access control with IAM
- you can use the IAM condition parameter `dynamodb:LeadingKeys` to allow users to access only the items where the partition key value matches their `user_id`