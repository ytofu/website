# S3 Bucket Accelerate Configuration

Manage S3 Bucket Accelerate Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    mybucket:
      bucket: mybucket

resource:
  aws_s3_bucket_accelerate_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      status: Enabled
```
