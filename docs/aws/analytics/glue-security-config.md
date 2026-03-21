# Glue Security Configuration

Configure encryption for Glue using ytofu YAML.

## Basic Security Config

```yaml
resource:
  aws_glue_security_configuration:
    example:
      name: example
      encryption_configuration:
        cloudwatch_encryption:
          cloudwatch_encryption_mode: DISABLED
        job_bookmarks_encryption:
          job_bookmarks_encryption_mode: DISABLED
        s3_encryption:
          kms_key_arn: ${aws_kms_key.example.arn}
          s3_encryption_mode: SSE-KMS
```
