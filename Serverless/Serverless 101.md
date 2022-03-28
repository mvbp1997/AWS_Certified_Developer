## Serverless 101
- allows you to run your application code in the cloud without managing any servers
- AWS handles infra management so you can focus on writing code
- AWS manages
  - capacity provisioning
  - patching
  - auto scaling
  - high availability
- Competitive Advantages
  - speed to market: by eliminating overhead of managing servers, you can release code quickly
  - super scalable: you can have a million users on your website and everything will scale automatically
  - lower costs: you never pay for over-provisioning; serverless apps are event-driven so you are only charged when your code is executed8
  - focus on your application: AWS offers a range of serverless technologies that work well together

### Example of Serverless Technologies
- Lambda: enables you to run code as functions without provisioning servers 
- SQS: simple queue service; a message queuing service that allows you to decouple and scale your app
- SNS: simple notification service; messaging service for sending text messages, mobile notifications, and emails
- API Gateway: allows you to create, publish, and secure APIs at any scale 
  - all about making your app accessible in a scalable and secure way
- DynamoDB: fully managed NoSQL database
- S3: object storage and web hosting

---
### Exam Tips: Serverless 101
- serverless: enables you to build scalable apps quickly without managing any servers
- low cost: serverless apps are event-driven and you are only charged when your code is executed
- AWS handles all the heavy lifting