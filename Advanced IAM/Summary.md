## Web Identity Federation
- allow users to authenticate with web identity providers (Google, Amazon, Facebook)
- user authenticates with webID provider, are given tokens, exchange the tokens for temporary AWS creds allowing them to assume an IAM role

## STS AssumeRoleWithIdentity
- STS: part of Security Token Service
- Authentication: allows users who have authenticated with web identity provider to access AWS resources
- API Call: after webId auth, the app makes the `assume-role-with-web-identity` API call providing the token generated by webId auth
- STS will then return temporary credentials enabling access to AWS resources
  - Within the response `AssumeRoleUser`, the ARN and the AssumedRoleID are used to programmatically reference temporary credentials, not an IAM role or user

## Cognito
- Cognito is an Identity Broker, handling interactions with web identity providers 
- Provides user sign-up and sign-in, and guest user access
- Recommended approach for mobile apps and web ID federation
- uses Push Synchronization (which uses SNS) to send silent push notifications of user data updates to multiple devices associated with a single user ID 

## Cognito User Pool and Identity Pool
- User Pool handles web ID federation brokerage 
  - receive JWT tokens
- Identity Pool exchanges the token for AWS credentials

## User Pool vs Identity Pool
User Pools
- user directories used to manage sign-up and sign-in functionality for mobile and web applications

Identity Pools
- enable you to provide temp AWS credentials 
- enabling access to AWS service 

## Inline vs AWS Managed vs Customer Managed Policies
- AWS Managed: policies created and managed by AWS for common use-cases (default)
  - cannot be modified
- Customer Managed: user created and managed policies
- Inline: managed by user, embedded in single user, group, or role
  - 1:1 mapping
  - deleting the user, group, or role also deletes the inline policy
- AWS recommends managed policy over inline

## Cross-Account Access
- allow access across multiple AWS accounts (prod vs dev)
- in Dev
  - create a group and a user, assign the user to the group
  - create an IAM policy that allows entity to assume the role you create in prod
  - attach policy to group
- in Prod
  - create AWS resource and a policy that allows access to that resource
  - attached the policy to an IAM role (which specified account ID of dev account)