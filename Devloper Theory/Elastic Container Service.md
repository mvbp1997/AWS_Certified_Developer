## Elastic Container Service: ECS
- fully managed container orchestration service that supports Docker and Windows containers
- quickly deploy and scale containerized workloads
- similar to Kubernetes, but with deep integration with AWS services

### Fargate vs EC2 for ECS
- EC2: ECS will run your containers on clusters of virtual machines
  - gives you more control of the configuration of your orchestration environment
- Fargate: serverless containers that you don't need to worry about the underlying EC2 instances

## Elastic Container Registry: ECR
- registry for container images
- ECS can connect to the registry to pull images to deploy

---
## Exam Tips
- Containers: virtual operating environment with everything the software needs to run
- allows apps to be built using independent, stateless components or microservices running in multiple containers 
- ECS: container orchestration service that will allow you to run your containers on a cluster of virtual machines
  - Fargate: serverless orchestration option
  - EC2: more control of your compute environment
- ECR: container registry; place to store your container images

---
## Deploying Containers with Elastic Beanstalk
- recap: Beanstalk allows you to deploy your application without needing to worry about the underlying infrastructure
  - handles capacity provisioning, load balancing, scaling, and application health monitoring
- Beanstalk supports the deployment of Docker containers
- you can either run a single container on a single EC2 instance or 
- you can run multiple Docker containers on each instance
  - Beanstalk will manage connections between the instances / containers by managing the ECS cluster
- when deploying code, upload the ZIP file containing all the code
- when upgrading the code, use the console to upload a new version and deploy
- code can be uploaded directly from your local machine or from a public S3 bucket
  - you can also use CodeCommit
