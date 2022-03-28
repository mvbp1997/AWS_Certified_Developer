Users = Identities you create with custom permissions that give individuals access to your AWS account

---
## Root User
- AWS account with unrestricted access to all resources
- Recommended NOT to use root user for everyday access

---
## IAM Users
- Individual IAM users within your account that correspond to to users in your organization
- Each user can have its own password for access to the AWS Management Console
- An IAM user does not have to represent an actual person; you can create an IAM user in order to generate an access key for an application that needs access to AWS resources

---
## Federating Users
- If the user has another way of being authenticated (ex. Active Directory), you don't have to create a separate IAM user for them
- You can *federate* user identities in AWS
- **Corporate Directory**
  - if compatible with SAML 2.0, you can configure the directory to provide SSO access to the Management Console
- **Internet Identity**
  - can also use OIDC provided by other parties (Facebook, Google, Amazon)

