## AWS Developer Tools
CodeCommit: Source & Version Control
- enable teams to collaborate on code and binaries

CodeBuild: Automated build service
- complies source code, runs tests, and produces packages 

CodeDeploy: Automated deployment service
- automate code deployment to EC2, Lambda, and on-prem

CodePipeline: manage build and deployment workflow
- end-to-end solution, allowing you to build, test, and deploy your code each time there is a change

---
## CICD 
- continuous integration: merging code changes frequently (CodeCommit)
- continuous delivery: automate building, test, and deployment (CodeBuild, CodeDeploy)
- continuous deployment: fully automated release process (CodePipeline)
- AWS Whitepaper: practicing continuous integration and continuous deployment on AWS

---
## CodeCommit
- centralized code repository
- enables collaboration and can manage updates from multiple users
- provides version control and version history

---
## CodeDeploy
- know the difference between in-place and blue/green
- in-place: take one or more instances offline while deployment is taking place
  - capacity is reduced during the deployment
  - lambda not supported
  - rolling back involves re-deploy
  - good for deploying for first time 
- blue/green: provision new servers and deploy once new servers pass health checks
  - no capacity reduction 
  - green instances can be created ahead of time
  - rollback is easy (switch load balancer)
  - you are paying for two environments in parallel (until you terminate the old servers)
- the appspec file: configuration file that defines parameters to be used by CodeDeploy (ex. OS, files, hooks, etc.)
- folder structure:
  - appspec.yml at the root
  - /Scripts: for script files
  - /Config: for additional config files
  - /Source: source files for app
- hooks: lifecycle event hooks have a very specific run order

---
## Lifecycle Event Hooks
- run order is very specific
- In-Place has broadly 3 phases
  - 1. de-register app with load balancer
  - 2. installation
  - 3. re-registration of app with load balancer 
- need to understand logical flow 

---
## CodeArtifact
- artifact repository, makes it easy to find software packages they need
- developers can find approved packages and can also publish their own 
- can also create an upstream repository with an external connection to pull packages from an external public repo

---
## CodePipeline
- continuous intergration/deployment process orchestrated by developer
- CodePipeline will trigger automatically when changes are detected
- can also integrate with AWS and Third-Party tools

---
## Containers
- virtual operating environment with everything software needs to run
- apps can be built using independent microservices running on containers

## Elastic Container Service
- ECS can run your containers on clusters of virtual machines
- Docker and Windows containers are supported
- Serverless Option: Fargate
  - can run containers without worrying about underlying EC2 instances 
- More Control Option: EC2
  - if you want to control the installation, configuration, and management of your compute environment
- ECR: Elastic Container Registry
  - where we can store container images

---
## Elastic Beanstalk
- you have the option of deploying a container to a single EC2 instance
- or deploy multiple to an ECS cluster 
- use Beanstalk to deploy Docker application
- you can easily upload and deploy a new version using the `upgrade` command
- code can be uploaded from your machine or S3

---
## CloudFormation
- allows you to manage, configure, and provision infrastructure as YAML, or JSON code 
- familiarize with different sections of the template
  - parameters: input custom values during formation runtime
  - conditions: provision resources according to the environment
  - resources (mandatory): describe the AWS resources that you want CloudFormation to create
  - mappings: allows you to make custom mappings (regions : AMI)
  - transform: allows you to reference code located in S3 (ex. reusable cloudformation code)
  - outputs: allows you to output values that other stacks may use/import 

---
## Serverless Application Model (SAM)
- define and provision serverless applications using CloudFormation
- `sam package`: packages your application and upload it to S3
- `sam deploy`: deploy your serverless app using CloudFormation

---
## CloudFormation Nested Stack
- allows you to re-use CloudFormation code 
- really useful for frequently used configuration code 
- reference it in your resources section as a new "Stack" type 
  - point it to where your template file can be found 
