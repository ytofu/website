# S3 Bucket Lifecycle Configuration

Manage object lifecycle rules for S3 buckets using ytofu YAML.

## Basic Lifecycle Rule

```yaml
resource:
  aws_s3_bucket:
    bucket:
      bucket: my-bucket

  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.id}
      rule:
        - id: rule-1
          status: Enabled
          filter:
            prefix: logs/
          transition:
            - days: 30
              storage_class: STANDARD_IA
            - days: 60
              storage_class: GLACIER
          expiration:
            days: 365
```

## Multiple Rules

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.id}
      rule:
        - id: archive-old-objects
          status: Enabled
          filter:
            prefix: data/
          transition:
            - days: 90
              storage_class: GLACIER_IR
          expiration:
            days: 730

        - id: cleanup-temp
          status: Enabled
          filter:
            prefix: tmp/
          expiration:
            days: 7

        - id: abort-incomplete-uploads
          status: Enabled
          filter: {}
          abort_incomplete_multipart_upload:
            days_after_initiation: 7
```

## With Tag Filter

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.id}
      rule:
        - id: archive-by-tag
          status: Enabled
          filter:
            tag:
              key: archive
              value: "true"
          transition:
            - days: 0
              storage_class: GLACIER
```

## Noncurrent Version Expiration

```yaml
resource:
  aws_s3_bucket_lifecycle_configuration:
    example:
      bucket: ${aws_s3_bucket.bucket.id}
      rule:
        - id: expire-old-versions
          status: Enabled
          filter: {}
          noncurrent_version_expiration:
            noncurrent_days: 90
            newer_noncurrent_versions: 3
          noncurrent_version_transition:
            - noncurrent_days: 30
              storage_class: STANDARD_IA
```
