# S3 Bucket Abac

Manage S3 Bucket Abac resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: bucket-name

resource:
  aws_s3_bucket_abac:
    example:
      bucket: ${aws_s3_bucket.example.bucket}
      abac_status:
        status: Enabled
```
