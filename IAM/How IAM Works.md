## Terms
- IAM Resources
  - user, group, role, policy, and identity provider objects stored in IAM
  - can add, edit, remove resources from IAM
- IAM Identities
  - resource objects used to identify and group 
  - ex. users, groups, and roles
  - you can attach a policy to an IAM identity
- IAM Entities
  - resource object used for authentication
  - ex. IAM users and roles

---
## Principal
A person or an application that makes a request for an action or operation on an AWS resource. 
- authenticated as an *IAM entity* to make request to AWS
- also support programmatic access to allow an application to access your AWS account

---
## Request
When a principal tries to use the AWS Management Console, API, or CLI, they send a *request* to AWS. Requests are gathered in a *request context* which is used to evaluate and authorize requests. Requests include the following information:
- **actions or operations** - what action or operation (create, edit, delete a resource) the principal wants to perform
- **resources** - AWS resource object upon which the action is performed
- **principal** - person or application that used an entity to send the request
  - information about principal includes *policies* associated with the entity assigned
- **environment data** - IP address, user agent, SSL enabled status, or time of day
- **resource data** - data related to the resource being requested (DynamoDB table name or an EC2 tag)


---
## Authentication
A principal must be authenticated (signed in to AWS) using their credentials to send a request to AWS. 
- To authenticate from the **management console** as an IAM user, provide your *account ID* or alias along with your *username* and *password*
- To authenticate from the **API** or **CLI**, provide your *access key* and *secret key*

---
## Authorization
In addition to being authenticated, the principal must also be *authorized* to complete the request. AWS uses values from the *request context* to check for policies that apply to the request. 
- Most policies are stored as [JSON documents](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#access_policies-json) and specify permissions for entities
- An *identity-based* policy is used for providing users with permissions to access AWS resources in their own account while a *resource-based* policy is used for granting cross-account access to a resource
- AWS checks each policy that applies to the context of your request
- AWS authorizes your request only if every part of your request is allowed
  - (explicit deny > explicit allow)


