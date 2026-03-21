# S3control Bucket Policy

Manage S3control Bucket Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3control_bucket_policy:
    example:
      bucket: ${aws_s3control_bucket.example.arn}
      policy: '{ "Id": "testBucketPolicy" "Statement": [ { "Action": "s3-outposts:PutBucketLifecycleConfiguration" "Effect": "Deny" "Principal": { "AWS": "*" } "Resource": aws_s3control_bucket.example.arn "Sid": "statement1" } ] "Version": "2012-10-17" }'
```
