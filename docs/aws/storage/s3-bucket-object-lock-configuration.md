# S3 Bucket Object Lock Configuration

Manage S3 Bucket Object Lock Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: mybucket

resource:
  aws_s3_bucket_versioning:
    example:
      bucket: ${aws_s3_bucket.example.id}
      versioning_configuration:
        status: Enabled

resource:
  aws_s3_bucket_object_lock_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        default_retention:
          mode: COMPLIANCE
          days: 5
```
