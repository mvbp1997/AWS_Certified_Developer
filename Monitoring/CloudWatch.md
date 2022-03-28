## CloudWatch
- a monitoring service to monitor the health and performance of your AWS resources, as well as applications that run on AWS and in your own datacenter
- CloudWatch can monitor
  - Computes: EC2, Elastic Load Balancers, Route53, Lambda
  - Storage and Content Delivery: EBS Volumes, CloudFront
  - Databases and Analytics: DynamoDB tables, ElastiCache nodes, RDS instances, Redshift, Elastic Map Reduce
  - Other: SNS topics, SQS queues, API gateway, estimated AWS charges
- CloudWatch Agent: used to define your own custom metrics
- CloudWatch Logs: used to monitor OS and application logs

### How it Works: CloudWatch and EC2
- all EC2 instances send key health and performance metrics to CloudWatch
- Default Host-Level Metrics: CPU, network, disk and status checks
  - metrics are stored indefinitely
  - you are able to retrieve data from EC2 or Elastic Load Balancer instances even after they have been terminated 
- OS-Level Metrics: memory usage, processes running, amount of free disk space, CPU idle time
  - by default, EC2 does NOT send OS level metrics
  - need to install CloudWatch Agent to collect OS metrics and send them to CloudWatch

### Metrics Frequency
- by default, EC2 sends metric data to CloudWatch in 5-minute intervals
- for an additional charge: you can enable detailed monitoring
  - send metrics at 1-minute intervals
- for custom metrics, default is 1-minute intervals
  - you CAN configure high resolution metrics that are sent at 1 second intervals
  - increasing frequency of metric collection = increased charges

### Monitoring System and Application Logs
- Monitor Log Files: monitor your app by using existing system and application log files
- Customizable: monitor logs in near real-time for specific phrases, values, or patterns 
  - requires the CloudWatch Agent
- Use Case: track the number of errors that occur, and create alert if threshold is breached

### CloudWatch Alarms
- create an alarm to monitor CloudWatch metrics in your account
- alarms can include: EC2 CPU utilization, ELB latency, charges on your AWS bill
  - set thresholds to trigger alarms and actions to be taken
- Use Case: you could set an alarm that sends a notification when 90% CPU utilization is reached, or it could execute an Auto Scaling policy 

--- 
## CloudWatch Exam Tips
- CloudWatch is all about monitoring the performance and health of your systems
  - default EC2 host-level metrics: CPU, network, disk and status check
  - use the CloudWatch Agent for operating system-level metrics: memory usage, processes, CPU idle time
- CloudWatch Logs: monitor and store application logs
- CloudWatch Alarms: create an alarm to monitor CloudWatch metrics in your account and generate an alert of take some action based on pre-defined thresholds

---
## Understanding CloudWatch Concepts
-  Metrics, Namespaces, Dashboards, and Dimensions

### CloudWatch Metrics
- metric = variable you would like to monitor
  - time-ordered sequence of values or data points which are published to CloudWatch
  - each data point in a metric has a timestamp
  - might also include optionally unit of measurement (ex. CPU Usage = percentage)
- metrics are uniquely defined by a name, a namespace and zero or more dimensions 

### CloudWatch Namespaces
- namespace = container for CloudWatch metrics
  - ex. EC2 uses "AWS/EC2" namespace
- you create your own namespace to publish custom metric data
  - specify a namespace for each data point or value that you publish
  - specify the namespace when you create a metric
- metrics in different namespaces are isolated from each other
- metrics from other applications are not aggregated into the same stats 

### CloudWatch Dimensions
- dimension = filter
- name/value pair that can be used to filter CloudWatch data
  - ex. use InstanceId dimension to search for metrics relating to a specific EC2 instance 
- CloudWatch can aggregate data across dimensions for some services like EC2

### CloudWatch Dashboards
- dashboard = custom view / page for monitoring CloudWatch metrics
- create a dashboard to display important metrics for all production systems in one place

--- 
## Exam Tips: CloudWatch Concepts
Understand the differences between the concepts
- Metrics: a variable to monitor (ex. CPU usage of an EC2 instance)
- Namespaces: container for metrics (ex. EC2 uses AWS/EC2 namespace)
- Dimensions: like a filter (ex. use InstanceId dimension to search for metrics related to a specific instance)
- Dashboards: custom home page you create to displace important metrics in one place 

---
## CloudWatch vs CloudTrail
- CloudTrail is a service that records all user activity in your AWS account
  - all events are recorded such as: creation, modification, or deletion of resources (such as IAM users, S3 buckets, and EC2 instances)
  - by default, you can view the last 90 days of account activity 
- CloudWatch is all about performance of metrics
  - CloudWatch Logs: application log monitoring
  - CloudWatch Alarms: alerts and actions based on metrics
- CloudTrail is all about monitoring AWS account activity
  - records API calls for your AWS account
  - delivers log files containing API calls to an S3 bucket 
  - 100% can be integrated with CloudWatch Logs (ex. failed log-ins can be tracked with CloudTrail sent to S3, then CloudWatch)
- Understanding the difference
  - Do you need to monitor the performance of your AWS Resources? --> CloudWatch
  - Do you need an audit log of all activity from an AWS Account --> CloudTrail

---
## Exam Tips: CloudWatch vs CloudTrail
CloudWatch: performance
- monitors performance and metrics of AWS resources
- uses CloudWatch Logs and CloudWatch Alarms

CloudTrail: audit trail
- records API calls for your AWS account
- API activity history related to the creation, deletion, and modification of AWS resources
- audit log of user activity in your AWS account

---
## CloudWatch Actions
The CloudWatch API
- supports long list of actions
- actions allow you to publish, monitor, and alert on a variety of metrics
- powerful when creating custom metrics for monitoring and alerting of your application

### PutMetricData
- publishes metric data points to CloudWatch
- you can define:
  - the name of the metric
  - the namespace to publish to
  - the value to publish 
  - the timestamp

### PutMetricAlarm
- creates an alarm associated with a metric when a threshold has been reached
- Ex. you want to be alerted if the average PageViewCount exceeds a threshold of 50 within a time period)

---
## Exam Tips: CloudWatch Actions
- Actions allow you to publish, monitor and alert on a variety of metrics 
- PutMetricData: allows you to publish metric data points to CloudWatch
- PutMetricAlarm: creates an alarm associated with a metric to alert you if a threshold is reached

