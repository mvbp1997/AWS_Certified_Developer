## Kinesis
- a family of services which enables you to collect, process, and analyze streaming data in real-time
- allows you to build custom applications for your business needs
- take action based on the data you are streaming
- Kinesis deals with data that is in motion (streaming) rather than static data (S3, DynamoDB, etc.)

### Streaming Data
- data generated continuously by thousands of data sources, which typically send data simultaneously in small sizes (KB)
- examples: financial transactions, stock prices, game data, social media feeds, location tracking, IoT sensors, log files, etc.
- all about high throughput information

### Four Core Services
- Kinesis Streams
  - stream data and video to allow you to build custom apps that process data in real-time
  - two main options: data streams and video streams
- Kinesis Data Firehose
  - allows you to capture, transform, and load data streams into AWS data stores to enable near-real-time analytics with BI tools 
- Kinesis Data Analytics
  - analyze, query, and transform streamed data in real-time using standard SQL; store the results in AWS data store
  - all about real-time analytics

### Kinesis Data Streams
Example
- data producers: source of the data (EC2, cellphone, laptop, IoT)
- all producers send data to Kinesis Streams
  - data is retained for default 24 hours (max 7 days)
  - data is stored in "shards"
  - shards = sequence of data records with each record having a unique sequence number
- data consumers: components that process the data
  - take the data from shards
  - can be anything from EC2 to Lambda functions
- after consumers process the data, they can send the data to storage solutions (DynamoDB, S3, RedShift, etc.)

### Kinesis Shards
- shards only apply to Kinesis Streams (not Firehose, or Data Analytics)
- streams are made up of shards
- each shard is a sequence of one or more data records and provides a fixed unit of capacity
  - each shard gets five reads per second
  - max total read rate of 2MB per second
  - 1,000 writes per second 
  - with a total of 1MB per second
- capacity of a Kinesis stream is determined by the number of shards it has
- as data rate increases, increase your number of shards

### Kinesis Video Streams 
- securely stream video from connected devices to AWS
- videos can be used for analytics and machine learning

### Kinesis Data Firehose
- no shards or streams
- all capacity and sizing is automated for you
- no need for consumers
- optionally can use lambda functions to analyze data in real-time as its coming in to Firehose
- no data retention
  - when data comes in, its either picked up and processed by lambda, or sent directly to S3/ElasticSearch
- automated setup (with Lambda to process data), straight to permanent storage with no consumers involved

### Kinesis Data Analytics
- allow you to run SQL queries as it comes in from Kinesis Firehose or Data Streams and store the results in permanent solution (S3, Elasticsearch, Redshift)
- this is all about real-time data analytics with standard SQL 

---
## Exam Tips: Kinesis
Understand the difference between each service:
Streams
- capture and store streaming video and/or data for real-time processing and analysis
- consumer applications process and analyze the data in real-time

Firehose
- capture, transform, and load data continuously into AWS data stores (or DataDog or Splunk)
- can integrate with BI applications for near real-time analytics of the stored data 

Data Analytics
- provide real-time analytics using standard SQL on data received by Kinesis Data Streams
- stores processed data in AWS data stores (S3, RedShift, or Elasticsearch)

---
## Kinesis Stream Demo
- a single EC2 running both producer and consumer Java Apps
- producer will write click event data to a Kinesis Data Stream
- consumer will read data from the stream and write it into DynamoDB

