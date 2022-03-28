## SQS
- Simple Queue Service
- distributed messaging queuing system
- allows you to decouple the components of an application so that they are independent
- SQS is pull-based not push-based
- Two types of SQS queue
  - standard
    - best-effort ordering
    - message delivered at least once
    - can occasionally see duplicates
    - default queue type
  - FIFO: first in first out
    - message order is strictly preserved
    - messaged delivered at least once (no duplicates)
    - good for transactions which need to happen in a strict order with no duplicates (banking)

### SQS Settings 
- visibility timeout: amount of time that the message is invisible in the queue after a reader picks up the message
  - default is 30 seconds (max value can be 12 hours)
- short polling: response is returned immediately even if no message are in the queue (even if empty)
  - cost is per response
- long polling: periodically poll the queue and only return a response when a message is in queue or a timeout is reached
  - most cost effective option

### SQS Delay Queue
- postpone the delivery of new messages
- set a delay period; messages remain invisible for this duration (0-900 seconds)
- great for large distributed applications that need to introduce delay in processing

### Large SQS Messages
- messages between 256KB and 2 GB are considered large
- use S3 storage to store these messages
- you will need SQS Extended Client Library for Java (for SQS message management) and the AWS SDK for Java (for S3 operations)

---
## SNS
- Simple Notification Service
- supports notification formats: SMS, SQS, HTTP, Email
- provides push notifications only
- operates using a pub/sub or publish and subscribe
- consumers need to subscribe to an SNS topic to get messages
- supports "Fanout" to send messages to large number of recipients

---
## SES
- Simple Email Service
- can use it to send and receive emails
- not subscription based; you only need to know the email address 

---
## SNS vs SQS
- SNS: messaging service; push-based; think push notifications
- SQS: messaging service; pull-based; think polling a queue for messages

---
## Kinesis 
Understand the difference between Kinesis services
- Streams (raw data): capture and store streaming video and data for real-time processing and analysis
  - consumer applications process the data and analyze in real-time
- Firehose (transform data): capture, transform, and load data continuously into AWS data stores (or other 3rd party providers)
  - existing BI tools can use near real-time analysis of the stored data
- Analytics: provides real-time analytics using standard SQL on data received by Kinesis Data Streams or Firehose and stores processed data in AWS data stores (S3, Redshift, Elasticsearch, etc.)

### Kinesis Shards
- Kinesis streams are made up of shards
- each shard is a sequence of one or more data records and provides a fixed unit of capacity within the stream
- data capacity of the stream is determined by the number of shards
  - increased data rate --> increase cap -->  increase number of shards 

### Kinesis Consumers
- need the Kinesis Client Library running on your consumers to run a record processor for each shard being consumed 
  - one record processor = one shard
- number of consumers should not exceed number of shards except for failover purposes 
- increasing the number of shards does not warrant an increase in number of processors 
  - instead use an auto-scaling group to drive scaling actions for your EC2 consumer instances

---
## Elastic Beanstalk
- use Beanstalk to deploy and scale web applications including your web application server platform
- supports languages: Java, PHP, Python, Ruby, Go, .NET, Node.js, etc.
- supports managed platforms: Apache Tomcat, Docker, etc.
- benefit of getting provisioned AWS services out of the box
- benefit of not having to manage system admin operations: OS and application server updates, monitoring, metrics, health checks, etc.
- benefit of having Beanstalk fully manage your EC2 instances for you
  - you also have the option to gain full admin control and customization of your EC2 instances

### Elastic Beanstalk Customization
For Amazon Linux 1
- use the `.ebextension` folder in the root of your directory
- files must have a `.config` extension

For Amazon Linux 2+ 
- use a Buildfile in the root directory for commands that exit upon completion (i.e. shell scripts)
- use a Procfile for custom long-running commands (i.e. commands to start your application)
  - note that Beanstalk will continuously try to restart the process if it has died
- use Platform Hooks for custom scripts or executables that run at various stages when EC2 is provisioned
  - use `.platform/hooks/[prebuild|predeploy|postdeploy]`

### Migrating an Existing .NET Application
- use the Windows Web Application Migration Assistant for Elastic Beanstalk
- formerly known as .NET Migration Assistant
- open-source, interactive PowerShell utility that migrates .NET applications from on-prem to Elastic Beanstalk

### Beanstalk Update / Deployment Types
All-At-Once: update all your instances at the same time
- involves service disruption
- rolling back will require a further All-At-Once update 

Rolling: new code is deployed in batches
- involves a reduced capacity during deployment
- rolling back will require a further Rolling update 

Rolling with additional batch: additional batch of instances is deployed where new code is updated
- maintains full capacity during update
- rolling back requires a further Rolling update 

Immutable: deploy a fresh set of new EC2 instances before destroying old instances
- maintain full capacity during update
- to roll back, delete the new instances and revert back to old ones (almost instance turnover)
- preferred option for mission critical production systems 

Traffic Splitting: performs Immutable deployment, but allows you to split incoming traffic between old and new deployment
- enables Canary testing: send small % of prod traffic to new version to test health without impacting all customers
- preferred option for mission critical production systems

---
## RDS and Elastic Beanstalk
- can either deploy RDS within or outside Beanstalk environment
- if within
  - quick and easy way to get started with database
  - downside is if Beanstalk environment is torn down, so is the RDS :(
  - suitable for Dev and Test environments only
- if outside
  - requires additional configuration (security group to enable port access, and RDS connection information strings)
  - upside is a teardown of the Beanstalk environment will have no impact on RDS
  - suitable for Production environments

