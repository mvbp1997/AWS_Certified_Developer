## SQS
- Simple Queue Service
- a message queue service
- enable web service apps to quickly and reliable queue messages that one component in the app generates for another component to consume
- queue: messages awaiting processing
- services can poll SQS to consume jobs/messages in the queue
- SQS is a "pull-based" system meaning a service MUST continuously poll the queue in order to consume the job/message
- the queue resolves issues that arise if 
  - the producer is working faster than the consumer
  - producer or consumer are only intermittently connected to the network

### Visibility Timeout
- when a message is first picked up by a service, it is marked as "invisible"
- "visibility timeout" refers to how long a service has to process the message
  - if the job does not complete within the timeout, the message becomes visible again
- SQS removes dependencies between components within the application
  - decoupling your infrastructure

### SQS Features
- Decouple App Components: so they can run independently, easing message management
- Store Messages: any component can store messages in the queue
  - messages can contain up to 256KB of text in any format
- Retrieve Messages: any component can retrieve messages programmatically
  - using the AWS SQS API 

### SQS as a Buffer
- a buffer between the component receiving the data for processing and the component creating/producing and saving the data

### SQS Key Facts
- SQS is pull-based
- messages can be up to 256KB in size
- messages can be made up of text data: XML, JSON, unformatted plain text
- guarantee: that the message will be processed at least once
- messages can be kept in the queue from one minute to 14 days 
  - default retention period is 4 days

--- 
## Exam Tips
- SQS is a distributed messaging queue system
- allows us to decouple components of an application so that they are independent 
  - good if components are prone to failure
- SQS is pull-based

---
## SQS Queue Types
- Two types of Queue: standard queues, FIFO queues
  - standard queues are the default, which provide best-effort ordering
  - FIFO (first-in-first-out), ordering is strictly preserved

### Standard Queue
- nearly-unlimited number of transactions per second
- guarantee messages delivered at least once
- best-effort ordering: ensure messages are generally delivered in the same order that they are sent
- occasionally more than one copy of a message might be delivered out-of-order 

### FIFO
- first-in-first-out delivery: order of messages is strictly preserved
- exactly-once processing: message is delivered once and remains available until a consumer processes and deletes it (duplicates not introduced)
- 300 TPS (transactions per second) limit
- good for banking applications (order of transactions is important)

---
## Exam Tips
Standard Queues
- best-effort ordering
- message delivered at least once
- occasional duplicates
- default queue type

FIFO
- first-in-first-out message order preserved
- messages delivered once
- no duplicates
- good for banking transactions which need to happen in a strict order

---
## SQS Settings
- visibility timeout: amount of time that the message is invisible in the SQS queue after a consumer picks up that message
  - default value is 30 seconds
  - you can increase this value as necessary
  - maximum value is 12 hours
- Short Polling: returns response immediately even if message queue being polled is empty
  - can result in a lot of empty responses
  - you will still pay for these responses (even if empty)
- Long Polling: periodically polls the queue
  - doesn't return a response until a message arrives in the queue or the long poll times out
  - generally preferable to short polling

---
## Exam Tips: SQS Settings
- visibility timeout: time the message is invisible in the SQS after a consumer picks up the message
  - default 30 seconds; max 12 hours
- short polling: response returned immediately even if empty (costs money)
- long polling: only return when a message is in the queue or if timeout is reached (saves money)

---
## SQS Delayed Queues & Managing Large Messages
- SQS delayed queues: postpone delivery of new messages 
- messages sent to the Delay Queue remain invisible to consumers for the duration of the delay period
- default delay is 0 seconds, maximum is 900 seconds
- for Standard Queues: changing the setting only affects new messages, not existing queued messages
- for FIFO Queues: this will affect the delay of messages already in the queue

### When to use a Delayed Queue
- large distributed apps that need delay in processing
- when you need to apply a delay to an entire queue of messages
  - ex. adding a delay of a few seconds to allow for updates to sales/stock controlling databases before notifying customers

### Managing Large SQS Messages
Best Practice for managing large SQS messages is to use S3
- large messages = 256KB up to 2GB in size
- you can use S3 to store the messages
- you need to use Amazon SQS Extended Client Library for Java to manage them
- you'll also need the AWS SDK for Java - provide API for S3 bucket and object operations

SQS Extended Client Library for Java allows you to:
- specify if messages are always stored in S3 or only those > 256KB
- send a message which references a message object stored in S3
- get a message object from S3
- delete a message object from S3

You need
- AWS SDK for Java
- SQS Extended Client Library for Java
- an S3 Bucket

---
## Exam Tips
SQS Delayed Queue
- postpone delivery of new messages
- messages in Delay Queue remain invisible for duration of delay period
- good for large distributed apps which may need to introduce a delay in processing

Managing Large Messages in S3 you need:
- AWS SDK for Java
- SQS Extended Client Library for Java
- an S3 Bucket