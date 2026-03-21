# Quicksight Key Registration

Manage Quicksight Key Registration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_quicksight_key_registration:
    example:
      key_registration:
        key_arn: ${aws_kms_key.example1.arn}
      key_registration:
        key_arn: ${aws_kms_key.example2.arn}
        default_key: true
```
