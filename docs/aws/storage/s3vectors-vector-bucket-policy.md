# S3vectors Vector Bucket Policy

Manage S3vectors Vector Bucket Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3vectors_vector_bucket_policy:
    example:
      vector_bucket_arn: ${aws_s3vectors_vector_bucket.example.arn}
      policy: |
        {
        "Version": "2012-10-17",
        "Id": "writePolicy",
        "Statement": [{
        "Sid": "writeStatement",
        "Effect": "Allow",
        "Principal": {
        "AWS": "123456789012"
        },
        "Action": [
        "s3vectors:PutVectors"
        ],
        "Resource": "*"
        }]
        }
```
