All the notes here are the exam tips for each section

## Serverless 101
- enables  you to build scalable applications quickly without managing any servers
- low cost: serverless apps are event-driven and only charge you when your code is executed
- AWS handles the heavy lifting: focus on writing code instead of configuring servers

## Lambda
- cost effective: only charged when your code executes
- continuous automated scaling
- event-driven
- independent (meaning each event will trigger a single function)
- serverless technology
- be aware of the different services that can trigger a lambda function (basically any serverless technology)
  - DynamoDB, Kinesis, SQS, App Load Balancer, API Gateway, Alexa, CloudFront, S3, SNS, SES, CloudFormation, CloudWatch, CodePipeline, CodeCommit

## API Gateway
- API is a front-door to your app
- provides an endpoint to your app running in AWS
- serverless: low cost and scalable automatically
- throttling: prevent your API from being overwhelmed with too many requests 
- CloudWatch: where everything is logged (API calls, latency, error, etc.)

## Lambda Version Control
- $LATEST is always the latest version of the code you uploaded
- use Versioning and Aliases to point your apps to a specific version of your code 
- example ARNs: `arn:aws:lambda:eu-west-2:1231254124:function:mylambda:Prod`
  - "Prod" is the version in this case
  - the entire ARN pointing to this version is the alias
- if your application uses an Alias, you will need to update it manually if you want to use the latest version of the code 

## Lambda Concurrent Executions Limit
- a limit does exists - 1,000 concurrent executions per second
- if you hit the limit, you will see a 429 Too Many Requests HTTP status code
- the remedy for this is to contact AWS Support to raise the limit
- Reserved Concurrency guarantees a set number of concurrent executions are always available to a critical function 

## Lambdas and VPCs
- you can enable Lambda to access resources in a private VPC
- you do this by providing the VPC Config information to your function
  - private subnet ID (where), and security group ID (with what permissions)
  - lambda will configure an Elastic Network Interface (ENI), using an IP from the private subnet CIDR range 
  - lambda will use the security group which will allow access to resources within the VPC

## Step Functions
- great tool to visualize and orchestrate serverless applications
- step functions automatically trigger and track each step of the State Machine or workflow
  - output of one step is the input to the next
- state machine = serverless technology
- step functions log the state of each step, making it easy to track and debug

## Comparing Step Function Workflows
Standard Workflows
- long-running (up to 1 year) 
- at-most-once
- non-idempotent (running an identical task will always cause a change in state)

Express Workflows
- short-lived processes (up to 5 minutes)
- at-least-once
- idempotent (running an identical task will not always cause a change in state)

Synchronous Express Workflow
- workflow must complete before the next step begins (ex. provide address before order can complete)

Asynchronous Express Workflow
- other tasks are not dependent on completion of workflow (ex. messaging system)

## X-Ray
- helps developers analyze and debug distributed application
- provides a visual representation of your application through a Service Map
- you must install the 
  - X-Ray Agent/Daemon to send logs to X-Ray as well as the 
  - X-Ray SDK to instrument your apps to send traces
- X-Ray is integrated with a lot of AWS Services (Serverless)
- you can also instrument your own applications to send data to X-Ray
- applications that can support X-Ray can run on 
  - EC2
  - Elastic Beanstalk
  - On-Premises
  - ECS
- when running X-Ray in ECS, be sure to run X-Ray daemon in its own Docker image running alongside your application
- X-Ray annotations (key/value pairs), provide you a way to define user-defined data which is indexed and can be filtered 

## API Gateway Caching
- caching improves performance of your API (latency) by caching the output of your API output
- reduces number of calls to your backend services, return cached output for identical requests
- TTL: time-to-live for cached data (default is 300 seconds or 5 mins)

## API Gateway Throttling
- default limits: 10,000 rps and 5,000 concurrent requests 
  - both limits are PER region
- error: 429 Too Many Requests
- use throttling to prevent your API from being overwhelmed by too many requests
- can also make a request to AWS Support to increase the limits

## Advanced API Gateway
- can import API definitions using external files such as OpenAPI (swagger)
- when dealing with legacy applications which use SOAP you can
  - configure your API Gateway as a SOAP web service passthrough
  - use your API Gateway to convert the XML response to JSON

