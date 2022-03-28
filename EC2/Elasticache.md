## ElastiCache
- memory is faster than disk
- In-Memory Cache (Key Value): makes it easy to deploy, operate, and scale 
- Improve database performance: it allows you to retrieve information from fast, in-memory cache instead of slow disk-based storage
- Great for Read-Heavy Database Workloads: caching the results of I/O intensive db queries
  - also good for storing session data for distributed apps

## 2 Types of Elasticache
### Memcached
- great for basic caching 
- scales horizontally, but there is no persistence, Multi-AZ or failover
- good choice for: if you want basic caching and you want your caching model to be simple

### Redit
- more sophisticated solution with enterprise features like persistence, replication, Multi-AZ, and failover
- support for sorting and ranking data (eg. gaming leaderboards), and complex data types like lists and hashes

### ElastiCache Scenario in the Exam
1. Database Under Stress: you will be given a scenario where a particular database is under a lot of stress
2. Find a solution: you may be asked which service you should use to alleviate
3. Know when to use ElastiCache: it is a good choice if your database is particularly read-heavy and not prone to frequent changing

### When ElastiCache CANT Help
1. heavy write loads: caching will not help alleviate heavy write loads; you may need to scale up your DB 
2. OLAP queries: if your DB is feeling stressed because you are performing Online Analytical Processing, think about using RedShift instead

--- 
## Exam Tips ElastiCache
- ElastiCache is an in-memory cache designed to improve read performance for read-heavy databases
- Memcached
  - in-memory, key-value store
  - object caching is your primary goal
  - you want things to be simple
  - you don't need persistence or multi-AZ
  - you don't need to support advanced data types or sorting
- Redis
  - in-memory, key-value store
  - you are performing data sorting and ranking
  - you have advance data types (lists and hashes)
  - you need data persistence and multi-AZ

--- 
## Systems Manager (Parameter Store)
- useful tool for storing parameters centrally and securely to be used by your applications (EC2 instances)
  - good for avoiding hard coded parameters
  - good for storing centralized secrets and configuration data
- two different tiers
  - Standard: 10,000 parameters; each with a value size of 4KB; free
  - Advanced: 10k+ parameters; each with up to 8KB; additional charge
- parameters can be passed by name to: CloudFormation, EC2, Lambda, CodeBuild, CodePipeline, etc.

--- 
## Exam Tips Parameter Store
- store confidential information: passwords, database connection strings, licence codes, etc
- plain text or encrypted
- pass by reference: you can reference parameters using the param name
- integrated with other AWS services: can be used with EC2, CloudFormation, Lambda, CodeBuild, CodePipeline, and CodeDeploy