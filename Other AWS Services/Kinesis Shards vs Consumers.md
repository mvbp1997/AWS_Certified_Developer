Recap:
- kinesis data stream is a set of shards
- shard is a sequence of data records in a stream, each data record has a unique sequence number
- data cap of your stream is sum total cap of its shards
- resharding = as your data rate increases, your number of shards also increases

### Consumers
- `kinesis client library` runs on the consumer instances
- tracks the number of shards in your stream
- discovers new shards when you reshard

### Kinesis Client Library
- the KCL ensures that for every shard there is a record processor
- manages the number of record processors relative to the number of shards and consumers
- if you only have one consumer, the KCL will create all the record processors on a single consumer
- if you have two consumers, it will load balance and create half the processors on one instance and half on another 
- consumer in this case refers to either an EC2 instance or Lambda, etc.
- processors are the processes running on the consumer

### Scaling Consumers