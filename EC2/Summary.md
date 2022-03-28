## EC2 - Exam Tips
- EC2 is like a VM that is hosted in AWS instead of your data centre
  - select the capacity that you need right now
  - grow and shrink when you need
  - pay for what you use
  - up and running in minutes, not months
- EC2 Instance Pricing
  - On-Demand: pay by the hour or second depending on the type of instance; 
    - great for flexibility
  - Reserved: reserve capacity for one or three years; up to 72% discount on hourly charge; 
    - great for well defined, fixed requirements
  - Spot: purchase unused capacity at a discount of up to 90%; prices fluctuate with supply and demand; 
    - great for apps with flexible start and end times
    - you define a price and if the SPOT price exceeds what you are willing to pay, it stops the instance
    - good for cost savings
  - Dedicated: a physical EC2 server dedicated for your use; 
    - great for server-bound licenses or compliance requirements
- Instance type determines the hardware of the host computer
  - each instance type offers different compute, memory, and storage capabilities
  - grouped into instance families
  - not necessary to remember all instance types
  - only thing to note: select instance type based on the requirements of your application

---
## EBS Volumes - Exam Tips
- highly available and scalable storage volumes that you can attach to your EC2 instance
- EBS = Elastic Block Store: SSD Volumes 
- IOPS = Input/Output Operations per Second
- GP2: General Purpose SSD
  - good for boot disks and general apps
  - up to 16k IOPS per volume
  - 99.9% durability
- GP3: Latest General Purpose SSD
  - good for boot disks and general apps
  - baseline 3k IOPS for all volumes
  - up to 16k IOPS per volume
  - 20% cheaper than GP2; want to encourage everyone to move to latest gen
- io1: Provision IOPS
  - suitable for OLTP and latency-sensitive apps
  - 50 IOPS/GiB
  - up to 64k IOPS per volume
  - high performance and most expensive
- io2: Latest Generation Provisions IOPS SSD
  - good for OLTP and latency-sensitive apps
  - 500 IOPS/GiB
  - 64k IOPS per volume
  - 99.999% durability 
- io2 Block Express: Provisioned IOPS SSD
  - for the largest, most critical, high performance apps (SAP HANA, Oracle, Microsoft SQL Server, IBM DB2)
  - up to 64TB of storage
  - 256k IOPS per volume 
  - SAN in the cloud performance
- st1: Throughput optimized HDD 
  - good for Big Data, data warehouses, ETL
  - max throughput is 500MB/s per volume
  - cannot be a boot volume
- sc1: Cold HDD
  - max throughput of 250MB/s per volume
  - less-frequently-accessed data
  - cannot be boot volume
  - lowest cost

## EBS Snapshots - Exam Tips
- EBS Snapshot: point in time copy of an EBS volume
  - great for backing up EBC volumes
  - can use snapshot to create new EBS volume
  - if you create a new EBS volume from an encrypted volume, you will get a new encrypted volume
  - same goes the other way with unencrypted volumes 

---
## Elastic Load Balancer - Exam Tips
- Application Load Balancers: load balancing for HTTP/HTTPS requests
  - routes request to a specific web server based on request type
  - ex. Car dealership website where you can route a request based on what info they want (service, parts, etc.)
- Network Load Balancers: provide high-performance load balance for TCP traffic
  - low-latency option
  - most expensive
- Classic Load Balancer: legacy option that supports both HTTP/HTTPS and TCP
- Gateway Load Balancers: provides load balancing for third-party virtual appliances
- X-Forwarded-For
  - if you need the IPv4 address of your end user, look for this HTTP header
- 504 Error: Gateway Timeout
  - end application is not responding within timeout period of load balancer
  - need to troubleshoot app

---
## Route53 - Exam Tips
- Amazon DNS Service
  - allows you to route a domain name to an EC2 instance, Elastic Load Balancer, or S3 bucket
- Route53 terminology
  - Hosted Zone: container for DNS records for your domain
  - Alias: allows you to route traffic addressed to the zone apex, or the top of the DNS namespace
    - ex. ilovecloud.com , and sent it to a resource within AWS
  - A record: allows you to route traffic to a resource using IPv4 address 

---
## AWS CLI - Exam Tips
- Principle of Lease Privilege: always give your users the minimum amount of access required to do their job
- best practice to use groups
  - create IAM groups and assign users to groups
  - group permissions are assigned using IAM policy documents
  - users will automatically inherit the permissions of the group
- Secret Access Key:
  - you will only see this once (on creation)
  - if you lose it, need to delete the access key ID and regenerate new ones
  - need to run `aws configure` to set it up on CLI
- don't share key pairs
  - each developer should have their own access key ID
- supports Linux, Windows, and MacOS and also works on EC2 instances

--- 
## Roles with EC2 - Exam Tips
- can use roles to give EC2 instance access to AWS resources (S3)
  - 1. create an IAM role (with access to desired resource)
  - 2. Create EC2 instance with role attached 
  - 3. Try to access resource from instance
- preferred option to grant roles to EC2 instances
  - avoid hard coding credentials and manual configuring them on instance
- use IAM policies to control permissions
  - can update policy attached to a role and it will take immediate effect on the EC2 instance
  - can attach and detach roles to running instances
- only 1 role per instance

---
## RDS - Exam Tips
- RDS database types: SQLServer, Oracle, MySQL, PostgreSQL, MariaDB, Amazon Aurora
- OLTP: Online Transaction Processing
- OLAP: Online Analytical Processing
- RDS is for OLTP workload
  - great for lots of small transactions (i.e. customer orders, banking transactions, payments, etc.)
- NOT suitable for OLAP
  - use RedShift for OLAP and data warehousing tasks (i.e. analyzing large amounts of data)

---
## Backups vs Snapshots - Exam Tips
Automated Backups
- automated, enabled by default, user-defined backup window
- point-in-time snapshot plus transaction logs to record DB
- retention period of up to 35 days
- can be used to recover your database to any point in time within retention period

DB Snapshot
- user-initiated, ad-hoc
- point-in-time snapshot only
- no retention period; stored indefinitely until user deletes them
- used to back up DB instance to a known state and restore to that specific state at any time 
  - ex. take a snapshot before making a change to a database

## RDS Encryption - Exam Tips
- enable encryption at time of creation
  - cannot encrypt an existing unencrypted RDS instance
  - encryption includes all underlying storage, automated backups, snapshots, logs, and read replicas
- KMS integration
  - uses AWS Key Management Service for AES-256 bit encryption
- to encrypt an unencrypted RDS instance, take a snapshot, encrypt the snapshot, then create a new RDS instance from the encrypted snapshot

--- 
## Multi-AZ vs Read Replica
Multi-AZ
- exact copy of production DB in another availability zone
- used for disaster recovery
- in the event of failure, RDS will automatically failover to standby instance

Read Replica
- a read-only copy of your primary DB in the same AZ, cross-AZ, or cross-origin
- used to increase or scale read performance
- great for read-heavy workloads and takes the load off your primary DB for read-only workloads

---
## ElastiCache - Exam Tips
- ElastiCache is an in-memory cache designed to improve read performance for read-heavy DB
- MemCached: in-memory, key-value data store
  - good for when
    - you want to keep things simple
    - object caching is your primary goal
    - you don't need data persistence or multi-AZ
    - you don't need to support advanced types like lists or hashes 
- Redis: in-memory, key-value data store
  - good for when
    - you want to perform data sorting and ranking (i.e. gaming leaderboards)
    - you have advanced data types (lists and hashes)
    - you need data persistence and you need Multi-AZ

---
## Parameter Store - Exam Tips
- service that allows you to store confidential information (i.e. passwords, DB connection strings, license codes, etc.)
- store values in plain text or encrypted
- you can then later reference the parameter using its parameter name (i.e. bootstrap script)
- integrated with AWS services (EC2, CloudFormation, Lambda, CodeBuild, CodePipeline, and CodeDeploy)