## SNS - Simple Notification Service
- a web service that makes it easy to set up, operate, and send notifications from the Cloud
- messages sent from an application can be immediately delivered to subscribers or other applications
- Use Cases:
  - push notifications to mobile devices
  - send SMS and Emails or even to AWS SQS or any HTTP endpoint
  - trigger lambda functions to process the information in the message, publish to another SNS topic, or send message to another AWS service

### How does it work?
- pub-sub model: publish and subscribe model
- applications can PUBLISH or PUSH messages to a TOPIC
- subscribers RECEIVE messages through a TOPIC
- TOPICS live within SNS to group SNS queue messages
- notifications are delivered using a push mechanism (eliminates need for periodic polling)

### What is a Topic?
- its an access point
- allow recipients to subscribe to and receive identical copies of the same notification
- SNS delivers appropriately-formatted copies of the message to each subscriber

### Durability Storage
- SNS enterprise feature that prevents messages from being lost
- all messages published to SNS are stored redundantly across multiple AZs

### SNS Benefits
- instantaneous, push-based delivery (no polling)
- simple APIs and easy to integrate with other AWS services and apps
- flexible message delivery over multiple transport protocols
- inexpensive, pay-as-you-go model with no up-front costs
- easy to configure using the AWS Console (point-and-click interface)
- offers high availability and durability features needed for production environment (managed services)

### Selecting the Right Solution (SNS vs SQS)
SNS
- messaging service
- SNS is push-based
- think of push notifications
- publish/subscribe model

SQS 
- messaging service; messages are held in a queue
- SQS is pull-based (needs a consumer and active polling)
- think of a polling consumer

---
## Exam Tips: SNS
- SNS: Simple Notification Service
- highly scalable and available notification service which allows us to send push notifications from the cloud
- supports variety of message formats: SMS, email, SQS, and HTTP endpoint
- runs on a pub-sub model where users/apps subscribe to the relevant TOPIC and a push mechanism to send out messages to the relevant TOPIC subscribers 
