## S3 Storage Classes
- availability = how available your S3 service is when you go to use it
- durability = how durable your data is; making sure it doesn't get lost of corrupted

### S3 Standard
- high availability and durability
  - data is stored redundantly across multiple devices in multiple facilities ( >= 3 AZs)
  - 99.99% availability and 11 9's for durability
- designed for frequently accessed data
- suitable for most workloads: is the DEFAULT storage class
- use cases
  - websites, content distribution, mobile and gaming apps, big data analytics

### S3 Standard-Infrequent Access (S3-IA)
- designed for infrequently accessed data
  - 99.9% accessibility
  - 11 9's durability
- rapid access: data that is accessed less frequently but required rapid access when needed
- pay to access the data
  - low per-GB storage price and per-GB retrieval fee
- use cases
  - long-term storage, backups, and disaster recovery
- minimum storage duration: 30 days

### S3 One Zone-Infrequent Access
- similar to S3-IA, but data is stored redundantly within a single AZ
  - 99.5% availability
  - 11 9's durability
- cost 20% less than regular S3-IA
- use cases
  - great for long-lived, infrequently access, non-critical data
- minimum storage duration: 30 days

### Glacier and Glacier Deep Archive
- glacier is very cheap storage
  - 99.99% availabilty
  - 11 9's durability
- optimized for data that is very infrequently access (archives)
- you PAY each time you access your data
- use cases
  - archiving data

Glacier
- provides long-term data archiving with retrieval times that range from 1 minutes to 12 hours 
  - ex. historical data only accessed a few times per year 
- minimum storage duration: 90 days

Glacier Deep Archive
- archives rarely accessed data with a default retrieval time of 12 hours
  - ex. financial records that may be access once or twice per year
- minimum storage duration: 180 days

### S3 Inteligent Tiering
- you are given 2 tiers: frequent and infrequent access
  - 99.9% availability
  - 11 9s durability
- automatically moves your data to most cost-effective tier based on how frequent you access each object
- great for optimizing cost
  - added monthly fee of $0.0025 per 1,000 objects

### Relative Cost
- **highest cost**: S3 Standard
- **cost optimized for unknown patters**: S3 Intelligent Tiering
- **retrieval fee applies**: S3 Standard-Infrequent Access, S3 One Zone-Infrequent Access, S3 Glacier, S3 Glacier Deep Archive

--- 
## Exam Tips
- know difference between each of the S3 storage classes and use-cases
- do not need to know durability, availability

S3 Standard
- use case: suitable for **most workloads**
  - ex. websites, content distribution, gaming apps, big data analytics
- available in >=3 AZ
- most expensive


S3 Standard-Infrequent Access (S3-IA)
- use case: long-term, **infrequently access critical data** 
  - ex. backups, data store for disaster recovery
- minimum storage duration: 30 days
- available in >=3 AZ
- cost is on retrieval fees

S3 One Zone-Infrequent Access
- use case: same as S3-IA but for non-critical data
  - also saves about 20% on costs if you don't need multi-AZ redundancy
- available in only 1 AZ

S3 Glacier
- use case: long-term **data archiving** that is occasionally accessed
  - retrieval time within a few **hours or minutes**
- available in >=3 AZ
- minimum storage duration: 90 days

S3 Deep Archive
- use case: **rarely accessed data archiving**
  - default retrieval time of 12 hours
  - ex. financial records for regulatory purposes
- available in >=3 AZ
- minimum storage duration: 180 days

S3 Intelligent Tiering
- use case: **unknown** or unpredictable access patterns
- most cost optimized (with a fee)
- available in >=3 AZ
- minimum storage duration: 30 days
