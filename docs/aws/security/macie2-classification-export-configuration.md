# Macie2 Classification Export Configuration

Manage Macie2 Classification Export Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_macie2_account:
    example:

resource:
  aws_macie2_classification_export_configuration:
    example:
      depends_on:
        - ${aws_macie2_account.example}
      s3_destination:
        bucket_name: ${aws_s3_bucket.example.bucket}
        key_prefix: exampleprefix/
        kms_key_arn: ${aws_kms_key.example.arn}
```
