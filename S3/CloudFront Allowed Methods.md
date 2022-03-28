## CloudFront AllowedMethods
- when you create a CloudFront distribution, you need to specify which HTTP methods your distribution will support
- GET, HEAD: read-only
- GET, HEAD, OPTIONS: read-only
- GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE: read-write

### Supported HTTP Methods
- GET: read data; read-only
- HEAD: inspect resource headers without reading the body; read-only
- PUT: send data to create a new, or replace a new resources (idempotent); write; ex. update status of resource
- PATH: partially modify a resource; write
- POST: insert data; used to create or update a resource (not idempotent); write; ex. comment on a blog post
- DELETE: delete data; write
- OPTIONS: used to find out what other HTTP methods are supported by given URL; read-only

### Which to use
- read-only: use GET, HEAD, and/or OPTIONS
- interactive website: use all the HTTP methods
  - restrict access at the origin level

---
## Exam Tips: CloudFront AllowedMethods
- only 3 options to choose from (2 read-only, 1 read-write)
- consider the needs of your website
- for interactive websites, use all HTTP methods and restrict access at origin level