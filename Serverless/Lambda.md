## Lambda
- serverless compute: run your code in AWS without provisioning servers
- lambda takes care of everything to run your code: including runtime environment 
- supported languages include: Java, Go, PowerShell, Node.js, C#, Python, and Ruby
- enterprise features included: auto-scaling and high availability

### Pricing
- you are charged based on the number of requests, duration, and amount of memory used by your function
- requests
  - first 1 million request per month are free
  - $0.20 per month per 1 million requests
- duration
  - you are charged in 1 ms increments
  - price depends on the amount of memory you allocate to your function
  - price per GB-second: $0.00001667 per GB-second
  - ex. function that uses 512MB for 100ms --> 0.5GB x 0.1s = 0.05 GB-seconds 
  - first 400,000 GB-seconds per month are free
- lambdas are VERY cost effective

### Event-Driven Architecture
- event-driven: lambda functions can be automatically triggered by other AWS services or called directly from any web or mobile app
- trigged by events: events can be changes to S3 bucket, or DynamoDB table
- trigged by user request: using API Gateway, you can configure an HTTP endpoint to trigger your function at any time using an HTTP request

### Amazon Alexa and Echo
- most Alexa skills run on lambda and are triggered by your voice 

### AWS Services that can Invoke Lambda
- DynamoDB, Kineses, SQS, Application Load Balancer, API Gateway, Alexa, CloudFront, S3, SNS, SES, CloudFormation, CloudWatch, CodeCommit, and CodePipeline

---
## Exam Tips: Lambda
- extremely cost effective: pay only when your code is executed
- continuous scaling: lambda scales automatically
- event-driven: lambda functions are triggered by an event or action
- independent: each event will trigger a single function
- lambda is serverless: it can easily integrate with other serverless technologies
- lambda triggers: multiple services can invoke a lambda function via triggers

---
## Lambda Versions
- when you create a Lambda function, there is only one version: $LATEST
- you can create multiple versions of your function code and use aliases to reference the version you want to use as part of the ARN
- an alias is like a pointer to a specific version of the function code
- each upload overrides $LATEST by default, to create a version from LATEST you have to do it in console, then create an ALIAS pointing to that new version
- arn:{alias} --> arn:$LATEST

--- 
## Exam Notes: Lambda Versions
- $LATEST is always the last version of code you uploaded to Lambda
- use Lambda Versioning and Aliases to point your application to a specific version if you don't want to use $LATEST
- if you application uses aliases, instead of $LATEST remember that it will not automatically use new code when you upload to it
  - only $LATEST is updated each time, you must create a new version each time and repoint your alias to said new version

---
## Lambda Concurrent Executions Limit
- there is a concurrent execution limit (don't need to know specifics for exam)
- safety feature / limit on number of concurrent executions across all functions in a given region per account
- default is 1,000 per region
- error message: TooManyRequestsException
  - HTTP Status Code: 429
- you can request to increase limit to the AWS Support Center
- reserved concurrency guarantees that a set number of executions which will always be available for your critical function 
  - this also acts as a limit

--- 
## Exam Tips: Concurrent Executions Limit
- know that a limit exists: 1,000 concurrent executions per second
- if you hit the limit, you will start to see invocations being rejected - 429 HTTP status code
- remedy is to raise limit through AWS support
- Reserved Concurrency guarantees a set number of concurrent executions are always available to a critical function