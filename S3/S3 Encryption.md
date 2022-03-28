## S3 Types of Encryption
- encryption in transit: encrypting data as it is coming/leaving your bucket
  - done using SSL/TLS, HTTPS (upload/download)
- encryption at rest - server side encryption: files encrypted in the bucket (you can encrypt existing files)
  - SSE-S3: S3 managed keys, using AES 256-bit encryption
  - SSE-KMS: AWS Key Management Service managed keys
    - additional layer of encryption on the keys
    - also comes with an audit trail so you can track key usage
  - SSE-C: customer provided keys
    - AWS manages encryption and decryption but user is responsible for lifecycle of keys
- encryption at rest - client side encryption
  - you can encrypt the files yourself before upload to S3

### 2 Ways Enforce Server Side Encryption 
- can use console to encrypt your bucket (just a checkbox)
- can also use a bucket policy

### Enforcing SSE for S3 Uploads
- every time a file is uploaded to S3, a PUT request is initiated
- if the file is to be encrypted during upload time, the `x-amz-server-side-encryption` header param will be included in the request
  - two options available: `AES256` (SSE-S3), `aws:kms` (SSE-KMS)
- when this param is included in the header of the PUT request, it tells S3 to encrypt the object at the time of upload

### Enforcing Encryption in Transit
- you can create an S3 bucket policy that requires encryption of data in transit (HTTPS, SSL, etc.)
- policy will explicitly deny any request that do not use `aws:SecureTransport`
- S3 will only serve content over HTTPS/SSL and deny all unencrypted HTTP access

---
## Exam Tips for S3 Encryption
- Encryption in Transit: encrypt data as it travels over the network
  - SSL/TLS, HTTPS 
- Encryption at Rest
  - server-side encrytpion
    - SSE-S3 (AES 256-bit)
    - SSE-KMS
    - SSE-C
  - client-side encryption
    - encrypt the files yourself before you upload to S3
- enforcing encryption using a Bucket Policy
  - explicitly deny request that do not include `x-amz-server-side-encryption` param in request header
  - deny requests that do not use `aws:SecureTransport` to enforce HTTPS/SSL
- can also enforce using console toggle