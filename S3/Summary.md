## S3 Summary
- object-based storage: allows you to upload files to AWS
- not suitable for OS or DB storage
- files can be up to 5TB in size
- unlimited storage
- files are stored in buckets
- S3 names are universal namespace
  - bucket-name.s3.Region.amazonaws.com/key-name
- successful CLI or API uploads will generate an HTTP 200 status code

## S3 Objects
- consist of a 
  - key (object name)
  - value (sequence of bytes)
  - version ID (versioning)
  - metadata (data about data, ex. content-type, last modified, etc.)

## S3 Storage Classes
- S3 Standard: suitable for most workloads (website, content distribution, mobile apps, big data analytics), and frequently accessed data
- S3 Standard-Infrequent Access: suitable for long-term, infrequently accessed critical data (ex. backups, disaster recovery, etc.)
  - minimum storage duration: 30 days
- S3 One Zone-Infrequent Access: same as S3 Standard-Infrequent Access except for non-critical data
  - minimum storage duration: 30 days
  - only stored in a single AZ
- S3 Glacier Instant Retrieval: suitable for long-lived data, accessed approximately once per quarter, but needs millisecond retrieval time
  - minimum storage duration: 90 days
  - cost effective way to store data, pay for every retrieval
- S3 Glacier Flexible Retrieval: same as S3 Glacier Instant, except data access can take a few hours or minutes. Suitable for data that is accessed occasionally
  - minimum storage duration: 90 days
- S3 Glacier Deep Archive: good for rarely accessed data archiving
  - retrieval time of 12 hours
  - minimum storage duration of 180 days
- S3 Intelligent-Tiering: designed for unknown or unpredictable access patterns
  - will automatically move infrequently accessed data to lower tier to save money

## Securing S3
- by default all newly created buckets are private
- Bucket Policies: applied at a bucket level 
- Access Control Lists (ACL): applied at an object level
- S3 buckets can be configured to create access logs (logs can be written to another bucket)

## S3 Encryption
- encryption in transit: encrypt data as it travels over the network (HTTPS, SSL/TLS)
- encryption at rest: server-side encryption (SSE)
  - SSE-S3 (AES 256-bit): S3 managed encryption keys
  - SSE-KMS: AWS KMS managed encryption keys
  - SSE-C: customer managed encryption keys
- client-side encryption: you can encrypt files locally before you upload them to S3
- enforce encryption with a bucket policy
  - explicitly deny request that do not include the `x-amz-server-side-encryption` parameter in the request header
  - deny requests that do not use `aws:SecureTransport` to enfore the use of HTTPS/SSL

## CORS
- Cross Origin Resource Sharing
- allow code in one bucket to access code/resource from another 

## CloudFront
- service to improve latency performance of a website by allowing you to cache your website in a geographically closer location to the users
- edge location: location where content will be cached (separate from AWS Region/AZ)
- origin: origin of all the files the distribution will serve
  - can be an S3 bucket, an EC2 instance, an Elastic Load Balancer, or a Route53 URL
- distribution: the origin and the configuration settings for the content you wish to distribute using CloudFront (CDN)
- edge locations are not READ only; they can be written to as well (i.e. PUT)
- S3 Transfer Acceleration: edge locations are utilized by S3 to reduce latency for S3 uploads
- Time To Live (TTL): objects are cached for the life of the TTL
  - by default this is 1 day, you can change this depending on how frequent your website changes
  - you can clear cached objects manually, but you will be charged

## CloudFront AllowedMethods
- defined the HTTP methods that your distribution will support
- 3 options to choose from (2 read-only, 1 read-write)
  - GET, HEAD, and/or OPTIONS
  - GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE
- consider the needs of your website
- interactive websites, use all HTTP methods (i.e 3rd option)

