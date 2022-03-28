## CloudFront
- content delivery network: system of distributed servers which deliver webpages and other web content
- easy and cost effective
- offers low latency and high data transfer speeds

### What is a CDN
- CDN = Content Delivery Network
- websites hosted on a server in a single geographical location will experience high latency
- introduce the concept of "edge location"
  - collection of servers distributed in multiple geographical locations
  - used to keep a cache (copy) of your website
- users can then access the edge locations instead of the main server; this will decrease latency
  - users local browser can also locally cache static pages


### CloudFront Terminology
- CloudFront Edge Location: location where content is caches; separate from AWS Region/AZ
- CloudFront Origin: origin of all the files that the distribution will serve; can be an S3 bucket, EC2 instance, Elastic Load Balancer, or Route53 address
  - optimized to work with other AWS services
  - can also integrate with other non-AWS origin server

- CloudFront Distribution: name given to the Origin and configuration settings for the content you wish to distribute using CloudFront 

### Improve the Performance of your Website
- use CDN to deliver your entire website using a global network of 200+ edge locations
- request for your content are automatically routed to the nearest edge location
- allows you to optimize performance for global website access

### Time to Live (TTL)
- objects are cached for a defined period of time TTL
- default is 1 day, when TTL is up, object is automatically cleared from cache
- if you clear an object from cache before TTL, you will be charged 

### S3 Transfer Acceleration
- this service works with CloudFront and enables fast, easy, and secure transfer of files over long distances between your end users and an S3 bucket
- upload file to edge location and route the object to AWS S3 over an optimized network path

---
## Exam Tips - CloudFront
- edge location: location where content is cached (separate from AWS Region/AZ)
- origin: origin of all files that the distribution will serve. Can be an S3 Bucket, EC2, Elastic Load Balancer, or Route53 address
- distribution: origin and configuration settings for the content we are distributing
- Edge locations are not just READ only; you can WRITE to them as well
- S3 Transfer Acceleration: use CloudFront to reduce latency for S3 uploads
- TTL: objects are caches for the life of the TTL; clearing cached objects manually before TTL, AWS will charge you

---
## Configuring Amazon CloudFront with Origin Access Identity
-  Origin Access Identity: a special "user" that can access the files in our S3 bucket and serve them to users
-  restrict public access to our origin and only allow access through CloudFront