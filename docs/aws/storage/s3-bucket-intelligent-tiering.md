# S3 Bucket Intelligent-Tiering

Configure intelligent tiering for S3 buckets using ytofu YAML.

## Basic Configuration

```yaml
resource:
  aws_s3_bucket_intelligent_tiering_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      name: EntireBucket
      tiering:
        - access_tier: DEEP_ARCHIVE_ACCESS
          days: 180
        - access_tier: ARCHIVE_ACCESS
          days: 125
```

## With Filter

```yaml
resource:
  aws_s3_bucket_intelligent_tiering_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      status: Enabled
      filter:
        prefix: documents/
        tags:
          priority: high
          class: blue
      tiering:
        - access_tier: ARCHIVE_ACCESS
          days: 125
        - access_tier: DEEP_ARCHIVE_ACCESS
          days: 180
```
