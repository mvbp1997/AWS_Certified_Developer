## SES
- SES = Simple Email Service
- scalable and highly available email service
- designed to help marketing teams and app developers send marketing, notification and transactional emails to their customers
- pay-as-you-go model
- send and receive emails (incoming mails can go to an S3 bucket)
- incoming emails from SES can be used to trigger lambda functions and SNS notifications 

### SES Use Cases
- automated emails (ex. notifications, online purchase confirmation)
- automated marketing emails

### SES vs SNS
SES
- email messaging service only
- can trigger a lambda function or SNS notification
- can be used for both incoming and outgoing emails
- an email address is all that is required to start sending messages 

SNS
- pub/sub messaging service that supports formats like SMS, HTTP, SQS, Email
- can trigger a lambda function
- can fanout messages to large number of recipients
  - replicate and push messages to multiple endpoints and formats 
- consumers must subscribe to a topic to receive the notifications

---
## Exam Tips: SES vs SNS
SES
- SES is for emails only
- SES can be used for both incoming and outgoing emails
- SES is not subscription based, all you need to know is the email address

SNS
- SNS supports multiple formats beyond email: SMS, HTTP, SQS
- SNS is for push notifications only; not for receiving
- SNS uses a pub/sub model
- SNS supports fanout (fanout messages to a large number of recipients with different formats)
- much more complex solution than SES