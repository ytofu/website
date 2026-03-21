# S3 Bucket Ownership Controls

Manage S3 Bucket Ownership Controls resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_s3_bucket_ownership_controls:
    example:
      bucket: ${aws_s3_bucket.example.id}
      rule:
        object_ownership: BucketOwnerPreferred
```
