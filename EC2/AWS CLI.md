## CLI Exam Tips
- principle of least privilege: always give your users the minimum amount of access required to do their job
- use groups
  - create IAM groups and assign your users to groups
  - group permissions are assigned using IAM policy documents
  - users will automatically inherit the permissions of their group
- secret access key
  - you only see the secret key once, if you lose it you can delete them and create new ones
  - after creating a new one, you will need to run AWS configure again
- don't share key pairs
- CLI is supported in Linux, Windows, and MacOS
  - you can install CLI on your local machine
  - alternatively you can also use EC2 instances (AWS CLI comes pre-installed)

---
## AWS CLI Pagination
- control the number of items included in the output when you run a CLI command
  - default for AWS CLI is 1000
- some errors you might see: timeout on API call
  - API call might be trying to fetch maximum number of items allowed (1000) but that might be too high
- some fixes available
  - use `--page-size` option to have CLI request smaller number of items from each API call
  - have the CLI make a larger number of API calls, each call retrieving smaller amounts of items with each call

## Exam Tips
- if you see errors related to timeout in the CLI command
  - adjust pagination of CLI result to avoid errors generated by too many results
  - CLI will still retrieve full list, but performs more API calls in the background 

## Launching an EC2 Instance with an S3 Role Exam Tips
- roles are the preferred option to manage security
- avoid hard coding your credentials 
  - roles allow you to provide access without use of access keys
- policies control a role's permissions
- you can update a policy attached to a role and it will take effect immediately
- attaching and detaching roles on a running instance will also take effect immediately 