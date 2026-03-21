# S3 Bucket Object Lock

Configure object lock for S3 buckets using ytofu YAML.

## Governance Mode

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: my-protected-bucket
      object_lock_enabled: true

  aws_s3_bucket_object_lock_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        default_retention:
          mode: GOVERNANCE
          days: 5
```

## Compliance Mode

```yaml
resource:
  aws_s3_bucket_object_lock_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        default_retention:
          mode: COMPLIANCE
          years: 3
```
