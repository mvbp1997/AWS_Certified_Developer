## CloudWatch Summary
- CloudWatch is all about monitoring the performance and health of your system
  - Default EC2 host-level metrics include: CPU, network, disk and status check
  - need to add a CloudWatch Agent for OS-level metrics: memory usage, processes, CPU idle time
- CloudWatch Logs monitors and stores your logs to help you better understand your systems and applications
- CloudWatch Alarms create alarms to monitor any CloudWatch metric in your account, generate an alert, or take some action

## CloudWatch vs CloudTrail
CloudWatch: Performance
- all about performance and metrics
- CloudWatch Logs: monitor logs
- CloudWatch Alerts: send alerts 
- use if you need to monitor performance of AWS resources

CloudTrail: Audit Trail
- all about recording the API calls for your AWS account
- records API activity history related to creation, deletion and modification of AWS resources
- also will record failed log-in attempts
- use if you need an audit log of user activity in your AWS account 

## CloudWatch Concepts
- Metric: is a variable to monitor (ex. CPU usage of an EC2 instance)
- Namespace: is a container for CloudWatch metrics (ex. EC2 uses AWS/EC2 namespace)
- Dimension: like a filter (ex. use InstanceId dimension to search for metrics relating to a specific EC2 instance
- Dashboard: a single custom home page that you create to display important metrics for your systems in one place

## CloudWatch Actions
- allow you to publish, monitor and alert on a variety of metrics
- `PutMetricData`: published data points to CloudWatch
  - ex. if your app keeps throwing CriticalErrors, use this command to log it to CloudWatch
- `PutMetricAlarm`: creates an alarm associated with a metric to alert you if a threshold has been reached