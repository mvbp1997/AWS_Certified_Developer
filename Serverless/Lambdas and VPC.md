## Lambdas and VPCs
- enabling Lambda to access your VPC resources (private)
- you need to allow the function to connect to the private subnet
- Lambda will need the following VPC config info:
  - private subnet ID
  - security group ID (with required access)
- Lambda will use this information to set up ENIs using an available IP address from your private subnet
  - ENI = Elastic Network Interface
- can add VPC config to Lambda using command line `vpc-config` parameter

```
aws lambda update-function-configuration --function-name {name} --vpc-config {SubnetIds=*,SecurityGroupIds=*}
```

---
## Exam Tips: Lambdas and VPCs
- possible to enable Lambda to access resources which are inside a private VPC
- provide VPC config to the function - private subnet ID, security group ID
- lambda uses VPC info to set up ENIs using an IP from the private subnet CIDR range
- security group then allows your function access resources in VPC