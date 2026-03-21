# S3 Bucket Intelligent Tiering Configuration

Manage S3 Bucket Intelligent Tiering Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket_intelligent_tiering_configuration:
    example-entire-bucket:
      bucket: ${aws_s3_bucket.example.id}
      name: EntireBucket
      tiering:
        access_tier: DEEP_ARCHIVE_ACCESS
        days: 180
      tiering:
        access_tier: ARCHIVE_ACCESS
        days: 125

resource:
  aws_s3_bucket:
    example:
      bucket: example
```

## Add intelligent tiering configuration with S3 object filter

```yaml
resource:
  aws_s3_bucket_intelligent_tiering_configuration:
    example-filtered:
      bucket: ${aws_s3_bucket.example.id}
      name: ImportantBlueDocuments
      status: Disabled
      filter:
        prefix: documents/
        tags:
          priority: high
          class: blue
      tiering:
        access_tier: ARCHIVE_ACCESS
        days: 125

resource:
  aws_s3_bucket:
    example:
      bucket: example
```
