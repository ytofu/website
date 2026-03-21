# S3 Bucket Server-Side Encryption

Configure server-side encryption for S3 buckets using ytofu YAML.

## SSE-S3 (AES-256)

```yaml
resource:
  aws_s3_bucket:
    mybucket:
      bucket: mybucket

  aws_s3_bucket_server_side_encryption_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      rule:
        apply_server_side_encryption_by_default:
          sse_algorithm: AES256
```

## SSE-KMS with Custom Key

```yaml
resource:
  aws_kms_key:
    mykey:
      description: This key is used to encrypt bucket objects
      deletion_window_in_days: 10

  aws_s3_bucket:
    mybucket:
      bucket: mybucket

  aws_s3_bucket_server_side_encryption_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      rule:
        apply_server_side_encryption_by_default:
          kms_master_key_id: ${aws_kms_key.mykey.arn}
          sse_algorithm: aws:kms
```

## SSE-KMS with Bucket Key

```yaml
resource:
  aws_s3_bucket_server_side_encryption_configuration:
    example:
      bucket: ${aws_s3_bucket.mybucket.id}
      rule:
        apply_server_side_encryption_by_default:
          kms_master_key_id: ${aws_kms_key.mykey.arn}
          sse_algorithm: aws:kms
        bucket_key_enabled: true
```
