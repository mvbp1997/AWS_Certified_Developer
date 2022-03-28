## Elastic Beanstalk
- deploy and scale web applications on servers without needing to provision (like EC2)
- supports many programming languages (Java, .NET, Python, etc.)
- supports many platforms (Apache Tomcat, Docker, etc.)
- developer benefits: focus more on code, worry less about underlying infrastructure needed to run the application
- provide code to Beanstalk and it will do the rest
  - create EC2 instance and auto scale groups
  - configure load balancers
  - create S3 buckets
  - create DynamoDB instances
- Beanstalk also integrates with CloudTrail and CloudWatch for app monitoring

### What Does Elastic Beanstalk Handle
- infrastructure
- application platform: installation and management of application stack
- you are in control: you have complete admin control
- "pay what you use" pricing model 

### Benefits for Developers
- let developers develop
- get apps to market faster
- devs don't need to worry about any underlying structure

--- 
## Exam Tips: Elastic Beanstalk
- quickest and easiest way to build and scale your web application (including web application server platform)
- supports many programming languages (Java, PHP, Python, Node.JS, .NET, etc.)
- supports many managed platforms (Apache, Docker, etc.)
- will also provision AWS resources for you
- will manage all system admin tasks for you
  - OS and application server updates, monitoring, metrics, health checks are all included 
- also allows full administrative control
  - fully manage the EC2 instances that Beanstalk creates

---
## Updating Elastic Beanstalk
Several Options for Development Updates
- all at once: deploys to all hosts concurrently
- rolling: deploys the new version in batches
- rolling with additional batch: launches an additional batch of instances; then deploys the new version in batches 
- immutable: deploys the new version to a fresh group of instances before deleting the old instances
- traffic splitting: installs new version on a new set of instances; forwards a percentage of incoming client traffic to a new application version for evaluation 

### All at Once Deployment
- deploys to all instances simultaneously 
- you will experience a total outage while deployment takes place
- no ideal for mission-critical production systems
- if the update fails, you will need to manually roll back the changes by re-deploying the original version to all your instances
- ideal for development and testing environments
  - easiest and simplest way of deployments

### Rolling Deployment
- deploys new version in batches
- each batch is taken out of service while deployment takes place 
- you won't experience a total outage
- however, your environment capacity will be reduced by the number of instances in a batch while the deployment takes place 
- not ideal for performance sensitive systems
- ideal for non-performance sensitive systems and you want to keep your service running during deployment
- if deployment fails, need to perform rolling updates to go back to working version

### Rolling With Additional Batch
- launch additional batch of instances, with the old version 
- deploys the new version on existing batches
- maintain full capacity throughout deployment
- if deployment fails, need to perform rolling updates to go back to working version
- ideal for performance sensitive systems that have 0 downtime
- not ideal for mission-critical systems where downtime due to a rollback is not desired 

### Immutable Deployments
- deploys new version to fresh group of instances
- only when new instances pass health checks do the old instances get terminated
- does not impact live environment
  - if new instances are unhealthy, just delete them and repoint load balancer to working instances
- ideal for mission-critical systems

### Traffic Systems
- extension of immutable deployments
- enables canary testing: test production environment by sending small % of traffic to new application version
- install new version on new set of instances
- forwards a % of incoming client traffic to new application version for a specified evaluation period 
  - if the new instances remain healthy, Beanstalk forwards all 100% of traffic to them and terminates the old version

---
## Exam Tips: Beanstalk Deployment Types
- need to know each version and what makes them different
- scenario based question, identify best option
- All at Once: deploy new version to all instances simultaneously
  - requires service interruption during deployment
  - rolling back requires a further All at Once update 
- Rolling: upgrade in batches
  - reduced capacity during deployment
  - rolling back requires a further Rolling update
  - good for non-performance sensitive apps
- Rolling with Additional Batch: upgrade in a batch of new instances before terminating old ones
  - maintain full capacity during deployment
  - rolling back requires further Rolling update 
  - not good for apps that require immediate rollback
- Immutable: deploy new batch of instances, only when health checks are complete do we terminate old instances
  - maintain full capacity during deployments
  - to roll back, delete new instances and repoint load balancer
  - good for mission-critical production systems
- Traffic Splitting: performs Immutable deployment and splits traffic between old and new instances
  - same benefits as Immutable deployment
  - enables Canary testing
