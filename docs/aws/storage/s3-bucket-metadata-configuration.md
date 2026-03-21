# S3 Bucket Metadata Configuration

Manage S3 Bucket Metadata Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket_metadata_configuration:
    example:
      bucket: ${aws_s3_bucket.example.bucket}
      metadata_configuration:
        inventory_table_configuration:
          configuration_state: ENABLED
        journal_table_configuration:
          record_expiration:
            days: 7
            expiration: ENABLED
```
