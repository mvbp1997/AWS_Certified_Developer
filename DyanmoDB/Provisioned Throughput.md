## Provisioned Throughput
- measured in capacity units
- when you create your table, you can specify your requirements in terms of read and write capacity units
  - defines how much data you can read and write to your table
- 1x write capacity unit = 1KB write per second
- 1x read capacity unit = 1x strongly consistent read of 4KB per second
- 1x read capacity unit = 2x eventually consistent reads of 4KB per second (default)
- if you app reads or writes larger items, it will consume more capacity units

---
## Exam Tips - Provisioned Throughput
- provisioned throughput is measured in capacity units
- write capacity: 1x = 1KB per second
- strongly consistent reads = 1x = 4KB per second
- eventually consistent reads = 2x = 4KB per second

---
## Provisioned Throughput Exceeded
- `ProvisionedThroughputExceededException`: your request rate is too high for the read/write capacity provisioned on your DynamoDB table
- the AWS SDK will automatically retry the requests until successful
- when not using the SDK:
  - reduce your request frequency in your application logic
  - use exponential backoff

### Exponential Backoff
- components are prone to being overloaded with concurrent requests
- usually will have clients hold retry logic
- when using the AWS SDK, in addition to simply retries, they also use exponential backoff
- exponential backoff = use progressively longer waits between consecutive retries, for improved flow control
- if requests still fail after one minute, your request size may be exceeding the throughput for your read/write capacity

---
## Exam Tips
- if you see the `ProvisionedThroughputExceeded` error, the number of requests is too high
- exponential backoff improves flow by retrying requests using progressively longer waits (improves flow control)
- exponential backoff is a feature of every AWS SDK command and applies to many serviecs (S3, CloudFormation, SES, etc.)