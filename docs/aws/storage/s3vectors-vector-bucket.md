# S3vectors Vector Bucket

Manage S3vectors Vector Bucket resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3vectors_vector_bucket:
    example:
      vector_bucket_name: example-bucket
```

## Encryption

```yaml
resource:
  aws_s3vectors_vector_bucket:
    example:
      vector_bucket_name: example-bucket
      encryption_configuration:
        sse_type: "aws:kms"
        kms_key_arn: ${aws_kms_key.example.arn}
```
