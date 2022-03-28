## Web Identity Federation
- simplifies authentication and authorization for web applications
- gives users access to AWS resources after successfully authenticating with web-based identity providers (ex. Google, Facebook, Amazon)
  - after successful auth, they will be provided an authentication code from the web ID provider
  - they can trade this auth code for temporary AWS security credentials

### Web ID Federation with Amazon Cognito
- Cognito: provides web ID federation including sign-up and sign-in
- Identity Broker: manages auth between your application and web ID provider 
- Multiple Devices supported (synchronize user data)
- Web Id Federation with Cognito is the recommended approach for authentication of mobile apps that communicate with AWS resources

### Authentication with AWS Cognito
- temporary credentials: brokers auth between Facebook, Amazon, Google
- temp credentials map to an IAM role, allowing access to required resources
- no need for the application to embed or store AWS credentials locally (secure and seamless)

### Cognito User Pools
- User Pools: user directories used to manage sign-up and sign-in functionality
- Sign-In: users can sign-in directly to the user pool, or using third-party web apps
- Identity Pools: enable you to provide temporary AWS credentials
  - enables access to AWS services like S3, or DynamoDB

### Cognito Push Synchronization
- synchronize data across multiple devices
- cognito tracks association between user identity and various devices they sign-in from
- cognito uses Push Synchronization to push updates and sync user data 
  - under the hood, uses SNS notification to all devices associated with a given user identity 

---
## Exam Tips - Web Identity Federation 
- allows users to authenticate with 3rd party web identity providers (Google, Facebook, etc.)
  - an authentication token (JWT) is exchanged for temporary AWS credentials (identity pool) 
  - temp AWS creds are mapped to an IAM role, giving users permission/access to AWS resources 
- Cognito acts as an Identity Broker handling interaction with web identity providers
  - user pool: provides sign-up and sign-in functionality
- Cognito is the recommended approach for web ID federation for mobile apps
- User Pool: user directories used to sign-up and sign-in users
- Identity Pool: enable you to provide temp AWS credentials
  - provides you the token to be able to access AWS resources 
- Cognito Push Synchronization: uses SNS to send silent push notification to multiple devices for data synchronization

---
## Cognito App Client
- what we use to call various Cognito APIs on our behalf