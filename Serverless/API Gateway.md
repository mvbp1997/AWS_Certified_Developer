## API Gateway
- Application Programming Interface
- service which allows you to publish, maintain and monitor APIs at any scale
- front door for apps to access data, business logic, or functionality from your backend services
- supported API types: RESTful APIs and Websocket APIs

### RESTful APIs
- Representational State Transfer
- optimized for serverless and web apps
- stateless
- they support JSON (Javascript Object Notation)
- API Gateway provides a single endpoint for all client traffic interacting with the backend of your application

### API Gateway
- what can it do?
  - allows you to connect to apps running in serverless services
- support multiple endpoints and targets
  - send each endpoint to a different target
- supports multiple versions
  - can maintain multiple versions of API for dev, prod environments
- serverless: cost effective and scalable
- CloudWatch: logs api calls, latencies, error rates to CloudWatch
- Throttling: helps manage traffic so backend operations can withstand attacks and high traffic

--- 
## Exam Tips
- API Gateway provides an endpoint to your applications running in AWS
- API is a front door to your app
- Serverless: Low cost and scales automatically 
- Throttling: throttle your API Gateway to prevent your app from being overloaded with too many requests
- CloudWatch: everything is logged (API Calls, latencies, and errors) sent to CloudWatch


