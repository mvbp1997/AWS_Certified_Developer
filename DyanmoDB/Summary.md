## DynamoDB
- DynamoDB is a low latency NoSQL database
- supports bot document and key-value data models
  - JSON, HTML, XML
- read operations are either eventually consistent of strongly consistent
  - eventually consistent 
- DynamoDB also allows for ACID transactions (DynamoDB Transactions)
  - ACID transactions = all or nothing (ex. credit card)
- DynamoDB Features
  - tables, items and attributes
- 2 Types of Primary Keys
  - partition key (unique identifier attribute) - customerID
  - composite key (partition key + sort key) - customerID + timestamp

## Access Control
- fine-grained access control with IAM
- IAM condition parameter `dynamodb:LeadingKeys` allows users to access only items where the partition key matches their User_ID

## Secondary Indexes
- enable fast queries on specific data columns
- give you a different view of your data based on alternative partition / sort keys
- Local Secondary Index
  - same partition key as table, but different sort key
  - can only be created when the table is created
- Global Secondary Index
  - different partition key and different sort key to your table
  - can be created any time

## Query
- query allows you to find an item in a Table
- using only the primary key attribute, you provide the primary key name and a distinct value to search for
- results are always sorted in ascending order by the sort key (if there is one)
- can always use the `ScanIndexForward` parameter to false to reverse the order of the query

## Scans
- scan operations examines every item in the table and by default returns all data attributes
- use the `ProjectionExpression` parameter to refine / filter the results 
- to make scans more efficient
  - set a smaller page size which uses fewer read operations
  - isolate scan operations to a specific table and segregate them from your mission-critical traffic
  - try parallel scans rather than default sequential scan (this will require more config up-front)
- query operations are generally more efficient than scans (don't read all attributes of every item, only read primary key)
- design tables in a way that you can use Query, Get or BatchGetItem APIs instead of scans

## Provisioned Throughput
- measured in capacity units
- write capacity unit = 1 x 1KB write per second
- strongly consistent read unit = 1 x 4KB per second
- eventually consistent read unit = 2 x 4KB per second

## On-Demand Capacity Pricing Model
- use this when you have unpredictable app traffic or want to use a pay-per-use model
- use Provisioned Capacity if 
  - read and write capacity requirements are forecasted
  - app traffic is consistent or increases gradually 

## DAX (DynamoDB Accelerator)
- provides in-memory caching for DynamoDB tables
- improves response times for eventually consistent reads only
- when a write operation occurs, data is written to both backend store and the cache at the same time
- point your API calls to DAX cluster instead of directly to your table
- cache hits on DAX = return data 
- cache miss on DAX = get data from table then store on DAX before returning
- not suitable for write-intensive applications or applications that require strongly consistent reads

## TTL (Time-To-Live)
- defines an expiry time on your data
- when an item is expired, it is marked for deletion (48 hours later)
- great for removing irrelevant or old data
- helps save money by automatically removing data that is no longer used by your application

## DynamoDB Streams
- time-ordered sequence of item level modifications in your DynamoDB tables
- sort of like an audit trail
- data in streams are encrypted and stored for 24 hours only
- good use case for Lambda event source

## Exponential Backoff
- `ProvisionedThroughputExceededException` error means the number of requests is too high (read/write)
- exponential backoff improves flow control by retrying requests using progressively longer waits
  - must be manually configured in application code
- standard feature in most AWS SDK commands (S3 Bucekts, CloudFormation, SES, etc.)

## AWS CLI Commands
- just know that CLI commands make calls to the DynamoDB API
- you must have the correct IAM permissions to make API calls