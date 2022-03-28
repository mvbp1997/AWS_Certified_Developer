## Identity Access Management
- IAM: used to define user access permissions within AWS
  - AWS Managed Policies
  - Customer Managed Policies
  - Inline Policies 

### AWS Managed Policies
- IAM policy created and administered by AWS
- provided for common use-cases based on job function
  - DynamoDBFullAccess
  - AWSCodeCommitPowerUser
  - AmazonEC2ReadOnlyAccess
- assign permissions to your users without writing the policies yourself
- attach to multiple users, groups or roles 
- you CANNOT change the permissions defined in an AWS managed policy

### Customer Managed Policy
- created by you and administered inside your own AWS account
- attach the policy to multiple users, groups, and roles within your account
- you can copy AWS managed policies and modify them to create your own custom policy
- recommended for use cases where the existing AWS policies don't fit the needs of your environment

### Inline Policy
- IAM policy embedded within the user group or role which it applies
  - when you delete the entity (user, group, etc), the inline policy is also deleted
- strict 1:1 relationship between entity and the policy 
  - cannot be attached to multiple entities (groups, roles, etc.)
- AWS recommends using managed policies over inline policies
- Recommended use case when the policy must NOT be inadvertently assigned to any other user, group, or role than the one for which it is intended
  - policy is only ever attached to one user, group, or role

---
## Exam Tips
- AWS Managed: created and managed by AWS (default) policies
- Customer Managed: created and managed by you
- Inline: managed by you, embedded in a single user, role, or group
- In most cases, AWS recommends managed policies over inline policies
  - only use inline when a policy must strictly be isolated to a single user, group, or role
  - deletion of the entity = deletion of the policy