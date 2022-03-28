## What is EC2?
- Elastic Compute Cloud 
- secure, resizable compute capacity in the cloud
- designed to make web-scale cloud computing easier for devs
- on-demand capacity
- complete control of your own instances

### Benefits of EC2
- pay only for what you use
- no wasted capacity
- set up a server in minutes instead of months

---

### Exam Tips
- EC2 is like a VM, hosted in AWS instead of on premises
- select the capacity you need now
- grow and shrink based on needs; pay for what you use
- wait minutes to set up instead of months

---
## EC2 Pricing Options
- on-demand pricing: pay by the hour or the second depending on the type of instance you run
- reserved: reserved capacity for one or three years; up to 72% discount on the hourly charge; instances operate regionally 
  - meaning if you reserve cap in one region and purchase cap in another region, you won't get the discount
- spot: purchase unused capacity at a discount of up to 90%; price fluctuate with supply and demand
  - you set a maximum price you're willing to pay for the instance; as soon as price exceeds max the instance is terminated/hibernated 
- dedicated: physical server running EC2 instances dedicated for your use (most expensive option)

### On-Demand
Good for applications that are...
- flexible; low cost and flexibility of EC2 without any up-front payment of long term commitment
- short-term; applications with short-term, spiky, un-predictable workloads that cannot be interrupted
- testing the waters; for apps being developed or tested on EC2 for the first time

### Reserved
Good for applications that are...
- predictable usage; apps with a steady state
- specific capacity requirements
- pay up-front; if you are able to make up-front payments 

There are three types of reserved instances
- standard RIs: reserve set quantity of a specific instance type (up to 72% discount)
  - one drawback is you cannot change the reserved instance types once you are locked in
- convertible RIs: similar to standard; except has the option to change to a different Reserved Instance type of equal or greater value (up to 54%)
- scheduled RIs: launch within the time window you define; match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, week, or month
  - schedule a time that works for your instance

### Spot
When to use SPOT instances...
- apps that have a flexible start-end time
- apps that are only feasible at very low compute prices
- users with urgent need for large amounts of additional computing capacity for small periods of time
  - ex. image rendering jobs, parallel work loads, complex calculations

### Dedicated
Good for applications that are...
- need to adhere to some sort of compliance; regulatory requirements that may not support multi-tenant virtualization
- licensing; for licenses that do not support multi-tenancy or cloud deployments 
- can be purchased on-demand or reserved 

### Saving Plans
- save up to 72% of all AWS compute instances regardless of type or region
- this is done by committing to use a specific amount of compute power (measured in $/hour) for one or three year period
- flexible; covers EC2 as well as Lambda and Fargate 

### AWS Pricing Calculator
- a calculator to help calculate price based on what instances you want
- [AWS Pricing Calculator](https://calculator.aws/#/)

---
### Exam Tips
- on-demand: pay by the hour or second depending on the type of instance you run; great for flexibility
- reserved: reserve capacity for one or three years; up to 72% discount on the hourly charge; great for well known, fixed requirements 
- spot: purchased unused capacity; great for applications with flexible start and end times; not great for apps that need to be up and running constantly
- dedicated: physical EC2 server dedicated for your use; great for server-bound license to reuse or compliance requirements

---
## Exploring EC2 Instance Types
- hardware: instance type determines the hardware of the host computer used for your instance
- capabilities: each type offers different compute, memory, and storage capabilities and are grouped in families
- application requirements: select the instance based on your application needs 
- wide selection to allow different use-cases and provide flexibility to choose a mix of appropriate instance types that fits everyones needs

### Different families of EC2 instances
- general purpose: balance of compute, memory, and network resources 
- micro instances: good for low cost, low throughput applications
- compute optimized: higher ratio of vCPU to memory; good for apps that require higher CPU (batch processing, high compute process)
- FPGA: hardware accelerated; good for apps that need massive parallel computing requirements
  - Field Programmable Gate Arrays
- GPU: widely used for apps that need parallel computing
  - Graphics Processing Unit
- machine learning: custom built CPUs optimized for running machine learning apps (image processing)
  - ASIC: application specific integrated circuit
- memory optimized: higher ratio of memory to vCPU; good for apps that require more memory storage (ex. database apps, cache, etc.)
- storage optimized: provides direct attached storage options; good for apps that require large storage (ex. noSQL databases, etc.)

---
### Exam Tips
- instance type determines the hardware configuration and capabilities of the host computer where the instance/VM is running
- each instance type provides a different compute, memory, and storage capabilities; grouped in families
- select the instance type based on the requirements of your application