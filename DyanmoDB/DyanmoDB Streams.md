## DynamoDB Streams
- time ordered sequence of item level modifications (ex. insert, update, and delete)
- records all logs and encrypts them at rest for 24 hours
- can be used for auditing or archiving or replaying a transaction
- could be used to trigger events as well (lambda)
- streams are accessed using a dedicated endpoint (Streams API) 
  - separate from the table endpoint
- by default, the primary key is recorded (default)
- you can also take snapshots (before and after images)
- Use Cases
  - audit or archive transactions
  - trigger an event based on a transaction
  - replicate data across multiple table 
- near real-time: apps can take actions based on contents of stream
- Lambda polls the DynamoDB stream and executes based on an event 

---
## Exam Tips
- Streams are time-ordered sequence of modifications of items in your table
- data is stored for 24 hours only
- can be used as an event source for Lambda

