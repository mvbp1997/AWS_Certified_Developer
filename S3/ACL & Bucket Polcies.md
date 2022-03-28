## S3 Demo
- versioning is a good way to protect against accidental deletion
  - it saves each new version of an object within the same bucket
- tags are good; defined by you; good for tracking and billing purposes
- theres also encryption! 
- object lock allowed as well: write-once-read-many (WORM) model

Note:
- just because you set the bucket policy to allow public access, doesn't mean its enabled by default
- you will still have to manually add a bucket policy to allow public access to your objects in the bucket
- make sure there are no ACL's blocking access as well, otherwise you will have to configure those as well

Note:
- by default, a policy with JUST the ARN will allow access to the bucket only
  - must add `/*` to the end to allow access to the buckets OBJECTS