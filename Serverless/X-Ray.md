## X-RAY
- tool which helps devs analyze and debug distributed apps
- provides visualization of your apps underlying components (X-RAY service map)
- X-Ray Service Map provides an end-to-end view of request as they travel through your application
- collects information such as: latency, HTTP status codes, and error messages

### X-Ray Integrations
- AWS Services: EC2, Elastic Container Services, Lambda, Elastic Beanstalk, SNS, SQS, DynamoDB, ELB, and API Gateway
- Integrate with your apps: Java, Node.js, .NET, GO, Ruby, Python
- API Calls: x-ray SDK automatically captures metadata for API calls made to AWS services using AWS SDK

### X-Ray Architecture
In order to get X-Ray working on your application:
- install X-Ray Agent: install agent on your EC2 instance
- configure: instrument your app using the X-Ray SDK
- the X-Ray SDK: SDK will gather information from requests and response headers, the code in your app, and metadata about the AWS resource on which it runs, and sends this trace data to X-Ray

## Exam Tips: X-Ray
- X-Ray is a tool used by developers to analyze and debug distributed applications
- the "Service Map" is a visual representation of your app
- X-Ray Agent and SDK must be installed on your AWS instance; use the SDK to instrument your app to send traces to X-Ray

---
### Demo Tips
- you can create apps from X-Ray (it will create CloudFormation stacks)
- in the "Service Map" you can drill down to individual components to see errors
- the Service Map provides an end-to-end view of requests as they travel through your application (Latency, HTTP status codes, errors)

---
## X-Ray Configuration Overview
- X-Ray SDK sends data to the X-Ray daemon which buffers segments into a queue and uploads them to X-Ray in batches
- you need both the SDK and the daemon running in your system where you application lives
  - daemon responsible for sending data
  - SDK responsible for collecting the data from your app (instrument)
- you can install the daemon on either:
  - EC2 instance or on-prem server
  - Elastic Beanstalk
  - on its own Docker container on your ECS cluster alongside your app

### Annotations and Indexing
- Annotations: when instrumenting your app, you can record additional info about requests 
  - key/value pairs that are indexed for use with filter expressions

## Exam Tips: X-Ray Configuration
- X-Ray integrates with many AWS services (DynamoDB, Lambda, API Gateway, etc)
- you can instrument your own apps to send data to X-Ray
- apps can be running on EC2, Elastic Beanstalk, on-prem, and ECS
- For ECS, run the X-Ray daemon on its own Docker image, running alongside your application
- you'll need three things before getting started:
  - X-Ray SDK
  - X-Ray Daemon
  - Instrument your app using the SDK to send the required data to X-Ray
- you can also record application specific information in the form of key-value pairs using Annotations 
  - this will allow you to filter, index and search within X-Ray



