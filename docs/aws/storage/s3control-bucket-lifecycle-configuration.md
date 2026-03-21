# S3control Bucket Lifecycle Configuration

Manage S3control Bucket Lifecycle Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3control_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3control_bucket.example.arn}
      rule:
        expiration:
          days: 365
        filter:
          prefix: logs/
        id: logs
      rule:
        expiration:
          days: 7
        filter:
          prefix: temp/
        id: temp
```
