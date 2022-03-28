## Cross-Account Access
- delegate access to resources in different AWS accounts
- manage/share resources between multiple accounts
- use IAM roles
  - create a role in one account to allow access and grant permissions to users in a different account
- switch roles: you can switch roles within AWS management console (no password required)

### Demo
- two environments production and development
- in development: 
  - create a IAM group and assign a user
  - create a policy (need prod account_id) to attach to the group (this will assume the role for the production account)
- in production:
  - create an IAM policy with access to an AWS resource
  - create a IAM role and attach the policy (need dev account_id)
- users in dev can then log into their console and select "change role" which will prompt them to log into the assumed role in production

