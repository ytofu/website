# S3 Bucket Request Payment Configuration

Manage S3 Bucket Request Payment Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket_request_payment_configuration:
    example:
      bucket: ${aws_s3_bucket.example.id}
      payer: Requester
```
