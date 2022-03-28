## CloudFormation
- service that allows you to manage, configure, and provision your AWS infrastructure as code
- resources defined using CloudFormation template
  - CloudFormation will make the appropriate API calls to create the resources in the template
- supports YAML or JSON template

### Benefits
- consistent: infrastructure is provisioned consistently with fewer mistakes (human error)
- quick and efficient: vs manual provision
- version control: version control and peer review for templates
- free-to-use: only charged for resources that you create
- manage updates and dependencies
- easy to roll-back to previous state and delete entire stacks

### CloudFormation Process
- YAML or JSON template to describe end state of infrastructure
- upload the template to an S3 bucket
- CloudFormation will read the template from the bucket and make the API calls (on your behalf) to create the resources
- CloudFormation Stack: resulting resources created from your template

### CloudFormation Template
- "Resources" section is mandatory
  - define the resources you want to create as part of your stack
- "Transform" section is for referencing additional code
  - reference additional code stored in S3, allowing for code re-use
  - ex. Lambda code, template snippets, reusable pieces of CloudFormation code, etc.

---
## Exam Tips - CloudFormation
- infrastructure as code: manage, configure, and provision AWS infra as YAML or JSON
- template
  - Parameters: input custom values
  - Conditions: provision based on environment 
  - Resources (mandatory): define AWS resources to create
  - Transform: reference code located in S3 (ex. Lambda, or reusable CloudFormation code)
  - Mapping: custom mapping, like Region : AMI

---
## Exporting CloudFormation Stack Values (Demo)
- exported variables in one stack can be leveraged by another stack 

--- 
## Serverless Application Model
- SAM is an extension to CloudFormation used to define and provision serverless applications
- SAM uses a simplified syntax for defining resources
- SAM CLI is used to packaged code, deploy code, upload to S3 bucket, etc.

### SAM CLI Commands
`sam package`: packages YAML template into a SAM compatible YAML template
- packages and uploads your template to S3
`sam deploy`: deploy the SAM compatible YAML template to CloudFormation
- takes a stack name and a capabilities parameter

---
## Nested Stacks
- allows you to re-use your CloudFormation code so you don't need to copy/paste them
- really useful for frequently used configurations (i.e. load balancers, web or application servers, etc.)
- reference it in your CloudFormation template using the Stack resource type