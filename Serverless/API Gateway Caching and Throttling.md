## API Gateway Caching
API Gateway can improve latency of your responses by caching the output of API calls to avoid calling your backend services each time
- caches your endpoints response: reducing the number of calls made to your endpoint and can also improve the latency for requests
- TTL: when you enable caching, API Gateway caches your responses from your endpoint for a specified time-to-live in seconds 
  - default is 300 seconds or 5 minutes

## API Gateway Throttling 
The purpose of throttling is to prevent your API from being overwhelmed by too many requests (DDOS)
- by default, API Gateway limits stead-state request rate to 10,000 requests per second, per Region
- the maximum number of concurrent requests is 5,000 requests across all APIs per Region 
- if you exceed 10,000 requests per second or 5,000 concurrent, you will get a 429 Too Many Requests HTTP response

---
## Exam Tips: Caching
- improve performance by caching the output of API calls to avoid calling your backend services; thereby reducing the number of calls to your backend services
- goal is to reduce LATENCY
- TTL: time-to-live for cached responses (default is 5 minutes, or 300 seconds)

## Exam Tips: Throttling
- default limit of 10,000 requests per second
- default limit of 5,000 concurrent requests per second
- if you exceed the limit, API Gateway will return 429 Too Many Requests error
- goal is to prevent your API from being overwhelmed by too many requests