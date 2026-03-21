# S3 Bucket Accelerate Configuration

Configure transfer acceleration for S3 buckets using ytofu YAML.

## Enable Transfer Acceleration

```yaml
resource:
  aws_s3_bucket:
    mybucket:
      bucket: mybucket

  aws_s3_bucket_accelerate_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      status: Enabled
```

## Suspend Transfer Acceleration

```yaml
resource:
  aws_s3_bucket_accelerate_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      status: Suspended
```
