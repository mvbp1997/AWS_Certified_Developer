## RDS
- relational database service
- relational databases:  data organized in tables, rows, and columns
- RDS is used for OLTP (Online Transaction Processing) workloads

### Types of RDS
- SQL Server
- Oracle
- MySQL
- PostgreSQL
- MariaDB
- Amazon Aurora (MySQL and PostgreSQL compatible; auto-scalable)

### Advantages
- up and running in minutes (with failover capability and automated backups)

### OLTP vs OLAP
- OLTP: Online Transaction Processing
  - process data from transactions in real-time 
  - eg. customer orders, bank transactions, payments, booking systems
  - OLTP is all about data processing, and completing large numbers of small transactions in real-time
- OLAP: Online Analytics Processing
  - process complex queries to analyze historical data
  - eg. analyzing profits, sales forecasting
  - OLAP is all about data analysis using large amounts of data, and complex queries that may take a long time to complete 
- Note: RDS is NOT suitable for OLAP or analyzing large amounts of data

--- 
## Exam Tips RDS
- RDS Database Types: SQL Server, MySQL, Oracle, PostgreSQL, MariaDB, Aurora
- RDS is designed for OLTP Workloads: great for processing lots of small transactions, like customer orders, banking, payments
- RDS is NOT suitable for OLAP; instead use RedShift for data warehousing; like analyzing large amounts of data, reporting, etc.

---
### Multi-AZ and Read Replicas
Multi-AZ: exact copy of your production database in another availability zone
- we have a primary RDS instance and a standby (secondary) instance located in a different availability zone
- standby instance is usually not visible to the application servers; in a situation where the primary fails, RDS automatically fail-over to the standby instance
- AWS handles all replication for you
- when writing to the primary database, writes are automatically synchronized to standby 
- all RDS types can be configured as Multi-ZA
- this is good for increasing data resiliency and disaster recovery
- not good for scaling out (cannot connect to primary and standby instances


Read Replica: read only copy of primary database
- great for read-heavy workloads; take read load off primary db
- a read-only replica can also be cross-region or cross-AZ
- each replica has its own DNS endpoint
- they can also be promoted to primary databases (note that this will break the read replication)
  - the new database will run independently of the primary
- good for scalability and increase performance
- requires automatic backup enabled in order to deploy a read replica
- multiple read replicas are supported (up to 5)

---
## Exam Tips Multi-AZ vs Read Replicas
Multi-AZ
- exact copy of prod db in another availability zone
- used for disaster recovery
- in the event of failure, RDS, will automatically failover to standby instance

Read Replica
- read-only copy of prod db in the same AZ, cross-AZ or cross-region
- used to increase or scale read performance
- great for read-heavy workloads and takes load off primary db (eg. business intelligence reporting)

---
## RDS Backups and Snapshots
Two ways to backup RDS
- database snapshot: manual, ad-hoc, and user initiated; provides snapshot of storage volume attached to DB instance
- automated backup: enabled by default; creates daily backups; transaction logs are used to replay transactions

### RDS Automated Backups
- point-in-time recovery: recover database to any point in time within a "retention period" of 1-35 days
- full daily backup: takes daily backup or snapshots and stores transaction logs throughout day
- recovery process: AWS will first choose the most recent daily backup and then apply transaction logs relevant to that day, up to recovery point
- automated backups and snapshots are stored in S3
- you get free storage space equal to the size of your database
- user-defined backup window
  - during backup window, storage I/O may be suspended for a few seconds, you may also see increase latency at this time

### Snapshots
- NOT automated, must be user-initiated manually
- no retention period; manual snapshots are NOT deleted, even when the RDS instance is deleted, including automated backups
- backup to a known state: can be done as frequently as you wish
- useful when: planned/known change to database, want to create "working" snapshot before executing change

### Restoring your DB
- whether restoring from a backup or snapshot, the DB will be completely new instance (with a new DNS endpoint)

### Encryption at Rest
- enable encryption during creation time
- integrated with KMS: encryption is done with AWS KMS (Key Management System) with standard AES-256 encryption
- includes all DB storage: all underlying storage, automated backups, snapshots, logs, and read replicas
- encryption can only be enabled DURING creation
  - you CANNOT encrypt an existing unencrypted instance
- to encrypt an unencrypted database, you will need to use a snapshot
  - encrypt the snapshot and create a new RDS instance with the encrypted snapshot

---
## Exam Tips Backups vs Snapshots
Automated Backup
- automated, enabled by default, you defined backup window
- point-in-time snapshot plus transaction logs to restore DB within retention period 
- retention period is user defined and within 1-35 days
- can be used to recover database to any point in time within retention period

DB Snapshot
- user-initiated, ad-hoc
- point-in-time snapshot only
- no retention period; stored indefinitely
- used to back up DB instance to known state and restore to a specific state in time

Encryption
- enable encryption at creation
  - includes underlying storage, automated backup
  - s, snapshots, logs, and read replicas
- uses KMS integration with AES-256 encryption
- to encrypt an unencrypted DB, use snapshots