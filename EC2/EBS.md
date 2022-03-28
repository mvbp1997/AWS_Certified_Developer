## What are EBS Volumes?
- Elastic Block Store
- storage volumes (disk) that you can attach to your EC2 instances
- each launched EC2 instance has at least 1 EBS attached (volume for OS)
- use them the same was you would use any system disk
  - create a file system
  - run a database / OS
  - install apps
  - store data

### EBS Features
- Production Workloads: designed for mission critical workloads
- High Availability: automatically replicated within a single availability zone to protect against hardware failures
- Scalable: dynamically increase capacity and change the type of volume with 0 downtime or performance impact on live systems

[EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)

### EBS Volume Types
- General Purpose SSD (GP2):
  - balance of price and performance
  - good for boot volumes or development and test apps which are not latency sensitive
  - GP3 is the latest generation (20% cheaper than GP2)
- Provision IOPS SSD (io1):
  - high performance, high cost option
  - use if more than 16,000 IOPS
  - designed for I/O intensive applications, large databases, and latency sensitive workloads
  - i02 is the latest generation; provides higher durability and more IOPS; same price as i02; 99.999% durability vs i01 (99.9%)
- i02 Block Express
  - provisioned IOPS SSD
  - SAN (storage area network) level performance in the cloud
  - highest performance, sub-millisecond latency (4x throughput, IOPS, and capacity of regular io2 volumes)
  - uses EBS Block Express architecture
  - great for large, most critical, high-performance applications like Microsoft SQL Server, Oracle, IBM DB2, SAP HANA, etc.
- Throughput Optimized HDD (st1)
  - low-cost HDD volume; cost effective way to store mountains of data
  - good for storage of HUGE amounts of data you might need to access frequently 
  - baseline throughput of 40 MB/s per TB; max throughput 500 MB/s per volume
  - good for frequently accessed, throughput-intensive workloads (big data, data warehouses, ETL, log processing)
  - Note: CANNOT be a boot volume; AWS won't let you
- Cold HDD (sc1)
  - lowest cost option
  - no where near as performant as st1
  - good choice for colder data requiring fewer scans per day
  - good for apps that need the lowest cost and performance is not a factor

### IOPS vs Throughput
- IOPS = Input/Output Operations per Second
  - measures the number of read write operations per second
  - important metric for quick transactions, low latency apps, and transactional workloads (reading/writing to DB, multiple changes, etc.)
  - ability to action reads and writes very quickly
  - if IOPS is important: choose IOPS SSD (io1 or io2)
- Throughput
  - measures the number of bits read or written per second (MB/s)
  - important metric for large datasets, large I/O sizes, complex queries
  - ability to deal with large datasets
  - if throughput is important: choose Throughput Optimized HDD (st1)

--- 

## Exam Tips
- EBS volumes are highly available and highly scalable storage volumes that you can attach to EC2 instances
- gp2 (General Purpose SSD)
  - suitable for boot disks and general applications
  - 3 IOPS per GiB
  - up to 16,000 IOPS per volume
  - up to 99.9% durability
- gp3 (Latest Generation General Purpose SSD)
  - similar to gp2 but has a baseline of 3,000 IOPS for all volumes
  - 20% than gp2
- io1: (Provisioned IOPS SSD)
  - suitable for online-transaction processing (OLTP) and latency-sensitive applications
  - 50 IOPS per GiB
  - up to 64,000 IOPS per volume
  - high performance and most expensive
  - up to 99.9% durability
- i02: (Latest Generation Provisioned IOPS SSD)
  - similar to i01, with increased IOPS and durability 
  - 500 IOPS per GiB
  - up to 99.999% durability
- i02 Block Expressed
  - for large, mission critical, high performance apps (SAP HANA, IBM DB2, etc.)
  - up to 256,000 IOPS per volume
  - up to 64 TB of storage
  - the only AWS SAN in the cloud offering
- st1: (Throughput Optimized HDD)
  - suitable for Big Data, warehouses, ETL
  - max throughput is 500 MB/s per volume
  - cannot be a boot volume
- sc1: (Cold HDD)
  - suitable for less-frequently-accessed data
  - max throughput is 250M MB/s per volume
  - lowest cost
  - cannot be boot volume
- encrypted snapshots: if you create an EBS volume from an encrypted snapshot, then the resulting EBS volume will also be encrypted 
- unencrypted snapshots: if snapshot is unencrypted, the resulting volume will also be unencrypted