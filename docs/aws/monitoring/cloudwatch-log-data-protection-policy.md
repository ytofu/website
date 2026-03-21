# Cloudwatch Log Data Protection Policy

Manage Cloudwatch Log Data Protection Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_s3_bucket:
    example:
      bucket: example

resource:
  aws_cloudwatch_log_data_protection_policy:
    example:
      log_group_name: ${aws_cloudwatch_log_group.example.name}
      policy_document: '{ "Name": "Example" "Version": "2021-06-01" "Statement": [ { "Sid": "Audit" "DataIdentifier": ["arn:aws:dataprotection::aws:data-identifier/EmailAddress"] "Operation": { "Audit": { "FindingsDestination": { "S3": { "Bucket": aws_s3_bucket.example.bucket } } } } }, { "Sid": "Redact" "DataIdentifier": ["arn:aws:dataprotection::aws:data-identifier/EmailAddress"] "Operation": { "Deidentify": { "MaskConfig": {} } } } ] }'
```
